---
layout: post
title: "A Whole New World"
date: 2012-10-26 07:42
comments: true
categories: 
- java
---
I started working at [Improving](http://improvingenterprises.com) this week which has required a major shift in my development ways. First and foremost is the change from PHP (which I've been coding for *years*) to Java. It wouldn't be so bad if it was *just* Java, though. However, that is not the case.
<!--more-->
Oh no, that is not the case by a *long* shot. I've been introduced to an entire new world consisting of jboss, maven, JSF, CDI, JPA, hibernate, and annotations, my God, the annotations!

Also Eclipse, but we won't go into that.

This past week has been such a head-stuffer that I'm certain I've lost some older, but valuable, information. (What's my wife's name again?) I'm going to quickly go over my experiences with each of these technologies and illustrate what my one week's worth of experience has left me with. I'll be doing so in no particular order.

CDI is pretty straight-forward. It's dependency injection (hence the "DI"). As long as you understand annotations, you're good. The main ingredient is `@Inject`, which does exactly that. It injects a dependency into a class, like this:

```java
import javax.inject.Inject;

public class MyClass {
    @Inject
    private SomeObject injectedObject;

    ...
}
```

This will instantiate `injectedObject` in the class so that it can be used in the class methods without any other preparation. Conceivably, you could then simply replace the SomeObject class with another in the class path and thus change what gets injected, for instance, a mock or stub class for testing purposes. This is made even easier (I think?) with some other annotations (like `@Qualifier`), which I'll get into later.

JPA and hibernate I'll cover together because hibernate is an implementation of the Java Persistence API (does anyone else get a kick out of nested acronyms, or is it just me?). I should mention that I'm working with hibernate 4 which, apparently, is significantly different from previous version from what I've been told. Hibernate is an ORM and used, obviously, for database access. It can be used with or without the persistence stuff; I am developing with persistence. 

Hibernate gave me a lot of trouble. At first it was easy, as I wrote my practice code in the "old style" using a config XML file. A couple hours of hacking away, and I was able to write to my database from my test application. Then I was told to convert that XML config file usage into annotations (which, humorously enough, require a *different* XML file). That's when all the trouble started.

I ran into many issues including:
* being told I need to wrap my calls to `persist()` (the method that inserts into the database) in transactions, 
* doing so, and being told that transactions can't be used (this and the previous led to a recursive loop of one then the other as I tried to fix both problems)
* finally getting no errors but not having the data actually be inserted into the database
* figuring out which versions of certain imported items I needed (there are some duplicates in both the javax.persistence and javax.transaction namespaces)

The second bullet point above lead to lots of research which essentially ended in my realizing that in order to use the `@PersistenceContext` annotation, you have to have the object using it declared as an EJB (Enterprise Java Bean), like so:

```java
import javax.ejb.EJB;

public class MyClass {
    @EJB
    private SomeObject objectThatPerformsCallsToPersist;

    ...
}
```

This is needed in order to inject EntityManager into the class that needs to call persist, using the `@PersistenceContext` annotation, like so:

```java
import javax.pesistence.*;
import javax.transaction.*;
import static javax.transaction.TransactionAttributeType.REQUIRED;

@Stateless
@Transaction(REQUIRED)
public class SomeObject {
    @PersistenceContext(unit="unit-name")
    private EntityManager em;

    public void addThing(thing) {
        em.persist(thing);
    }
}
```

You'll notice a few things here. We set transactions as required, which will wrap all database calls in transactions if they aren't already. This is for the first bullet point above. Second, we set as `@Stateless` in order to make this available to CDI (that's a whole different set of explanations). You'll see what we set the EntityManager to persist. I'm *pretty sure* this means there's only one hanging around (we aren't recreating new ones every time we need one), but I *do* know that the `@PersistenceContext` essentially injects the EntityManger in. Also, you'll see the unit was set to some string. This must match a `<persistence-unit>` you've set in persistence.xml.

Yeah, so that was the gist of how I got it working after about a day. Then I'm told "oh, you shouldn't need the `@EJB` annotation, so practice fixing/refactoring that out". So I did, taking about another half of a day and eventually breaking down and having my manager/superior type person help me out. Long story short, it turns out that `@PersistenceContext` requires `@EJB` in the mix, but `@PersistenceUnit` does not. So, changing the former to the latter lets you not need the `@EJB` annotation, also requiring some other changes.

*Or so we thought.*

The final result that ended up working without needing @EJB looks like this:

```java
@Named
@RequestScoped
@TransactionAttribute(REQUIRED)
public class SomeAction {
    @Inject
    private ObjectPersister persister;

    private String storedString;

    public void doSomething() {
        persister.addToDb("String to add.");
        storedString = "String to store.";
    }
}
```

The `doSomething()` method is meant to be called from an HTML element (such as a button) via JSF. The `@Named` annotation allows the .xhtml file(s) to reference `{someAction.doSomething}`. `@RequestScoped` is the scoping I used for my test application. This is just a string that gets set then displayed in the web browser (explained later).

However, we need our `ObjectPersister` class;

```java
import javax.persistence.*;
import javax.transaction.*;
import javax.ejb.*;
import static javax.ejb.TransactionAttributeType.REQUIRED;

@Stateless
@TransactionAttribute(REQUIRED)
public class ObjectPersister {
    @PersistenceContext(unitName="my-unit")
    private EntityManager em;

    public String addToDb(String stringToAdd) {
        MyObject myObject = new MyObject(stringToAdd);
        em.persist(myObject);
        return myObject.theString;
    }
}
```

This is similar to my example above. Fairly straight forward. However, we need our `MyObject` class:

```java
import javax.persistence.*;
import java.io.Serializable;

@Entity
@Table(name="quote")
public class MyObject implements Serializable {
    @Id
    @GeneratedValue
    @Column(name="id")
    private Integer id;

    @Column(name="theString")
    private String theString;

    public MyObject() {
    }

    public MyObject(String str) {
        theString = str;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getTheString() {
        return theString;
    }

    public void setTheString(String str) {
        theString = str;
    }
}
```

This class is straight forward; it's basically just a bean. The `@Entity` annotation essentially labels it as a database object (single entry, sort of), and the `@Table` gives the database table name these objects should be written to. The rest is mostly self-explanatory.

Ah, but we're still missing a piece to the puzzle. Remember that "unit" from before? We need to define that, and we do so in our persistence.xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence xmlns="http://java.sun.com/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://java.sun.com/xml/ns/persistence http://java.sun.com/xml/ns/persistence/persistence_2_0.xsd"
             version="2.0">

  <persistence-unit name="my-unit">

    <jta-data-source>java:jboss/datasources/MySqlDS</jta-data-source>
    <properties>
      <property name="hibernate.dialect" value="org.hibernate.dialect.MySQLDialect" />
      <property name="hibernate.hbm2ddl.auto" value="update"/>
      <property name="hibernate.show_sql" value="true" />
    </properties>

  </persistence-unit>
</persistence>
```

In this case, I'm using MySql. The third property, when set to "true" will print all database queries that are run to jboss' console, which is good for debugging. See that `<jta-data-source>`? Yeah, we need that. Turns out that *that* needs to be defined in the jboss config (not an application specific config)! Here's an example:

```xml
<datasources>
    <datasource jndi-name="java:jboss/datasources/MySqlDS" pool-name="MySqlDS">
        <connection-url>jdbc:mysql://localhost:3306/quotes</connection-url>
        <driver>com.mysql</driver>
        <transaction-isolation>TRANSACTION_READ_COMMITTED</transaction-isolation>
        <pool>
            <min-pool-size>10</min-pool-size>
            <max-pool-size>100</max-pool-size>
            <prefill>true</prefill>
        </pool>
        <security>
            <user-name>username</user-name>
            <password>password</password>
        </security>
        <statement>
            <prepared-statement-cache-size>32</prepared-statement-cache-size>
            <share-prepared-statements>true</share-prepared-statements>
        </statement>
    </datasource>
    <drivers>
        <driver name="com.mysql" module="com.mysql">
            <xa-datasource-class>com.mysql.jdbc.jdbc2.optional.MysqlXADataSource</xa-datasource-class>
        </driver>
    </drivers>
</datasources>
```

You'll need to add these to your `<datasources>` and its `<drivers>` section. I added them to jboss' standalone.xml, but apparently you can add them to a domain-specific config as well.

Now we only have one more thing. Since I'm using maven, I need to add the appropriated dependencies to my pom.xml file:

```xml
<dependencies>
   <dependency>  
     <groupId>javax.persistence</groupId>  
     <artifactId>persistence-api</artifactId>  
     <version>1.0-rev-1</version>  
   </dependency>  

   <dependency>
     <groupId>javax.transaction</groupId>
     <artifactId>jta</artifactId>
     <version>1.1</version>
   </dependency>
</dependencies>
```

Add these to your `<dependencies>` tag.

After all of this, you *should* be set! The only thing missing is the .xhtml file to use the action from above, but I'll get to that below.

*Whew* Moving on...

Since I've mentioned them, jboss and maven are just part of the architecture. jboss is the server and maven acts as both a builder (like make) and a dependency manager. Not much else to say right now.

Finally, we get to JSF: Java Server Faces (I believe). This, from what I can tell, is a templating engine to let your .xhtml files access your Java classes (via the `@Named` annotation as mentioned).

Here's the missing example from our code/setup above:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
   "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml"
   xmlns:ui="http://java.sun.com/jsf/facelets"
   xmlns:h="http://java.sun.com/jsf/html"
   xmlns:f="http://java.sun.com/jsf/core">

<h:head>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
<title>My App</title>
</h:head>

<body>
   <div id="content">
      <div>
        <h:form id="myForm">
          <h:commandButton id="myButton" value="Click Me">
            <f:ajax event="click" render="targetElement" listener="#{someAction.doSomething}"/>
          </h:commandButton>
          <h:outputText value="#{someAction.storedString}" id="targetElement"/>
        </h:form>
      </div>
   </div>
</body>
</html>
```

So, what we have here is a button that runs the `someAction.doSomething()` method, the renders the `targetElement` element when it is done. The `targetElement` has a value equal to whatever `someAction.storedString` is, so when `someAction.doSomething()` changes its value and tells `targetElement` to render, the value displayed in the browser changes to the new value set in the class. JSF provides the `#{}` interface between xhtml and Java classes.
<hr />
I'll be honest, my biggest issue and the reason it took me almost two days to do what I did is old information on the Internet. We are using basically the latest and greatest, so I had to make sure that the information I was reading was jboss 7, hibernate 4, etc. Wading through all the old stuff wasn't easy, though search filters helped. Also, we don't use Spring so I had to make sure I added "-spring" to my searches, especially when looking up persistence and transaction things. 

Once you've filtered out all the crud, then you find the mess: several different posts showing you several different ways to achieve a particular goal. If you're like me, none of them will work right, and you'll be left picking out the pieces of each that do and trying to smash them together into something coherent that works. (Then, if you're *really* like me, you fail, get frustrated, and ask for help.) However, the entire experience, through frustrating, leaves you with much more knowledge than you had before.

Well, that's all for now. Hopefully I'll be able to put my newly-obtained information to good use.