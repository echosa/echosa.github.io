---
layout: post
title: "Triangle Game Update"
date: 2012-09-09 18:12
comments: true
categories: 
- java
- triangle
---
So, I've recently pushed a number of changes to my Triangle Game project I'm using to learn Java again. Updates include:

* Bug fixes and display improvements
* Various effects that are randomly assigned to the spaces on the board
* Missing turns (after landing on spaces with that effect)
* Refactored code
<!--more-->
Specifically, I'm pretty proud of the randomly assigned space effects. I achieved this using a technique that I also use in my test script. The test script will automatically pull in all test classes, given they are in the right directory and package. In order to randomly assign effects to the board I do something quite similar. Each time I create a space to assign to the board (except the first and last spaces), I make a call `Play.getRandomEffect()`, which looks like this:

```java
public static SpecialEffectInterface getRandomEffect()
{
    List<String> effectClasses = new ArrayList<String>();

    File thisPath = new File(SpecialEffectInterface.class.getResource("SpecialEffectInterface.class").getPath());
    String thisPackage = SpecialEffectInterface.class.getPackage().getName() + ".";

    File dir = new File(thisPath.getParent());
    File[] children = dir.listFiles(new EffectFilter());
    if (null != children) {
        for (int i=0; i<children.length; i++) {
            String filename = children[i].getName();
            effectClasses.add(thisPackage + filename.substring(0, filename.length()-6));
        }
    }
    int choice = 0 + (int)(Math.random() * (effectClasses.size() - 1));
    String classChoice = effectClasses.get(choice);
    SpecialEffectInterface effect = null;
    try {
        effect = (SpecialEffectInterface) Class.forName(classChoice).newInstance();
    } catch (ClassNotFoundException e) {
        System.out.println("Class Not Found: " + e.getMessage());
        System.exit(1);
    } catch (InstantiationException e) {
        System.out.println("Instantiation Exception: " + e.getMessage());
        System.exit(1);
    } catch (IllegalAccessException e) {
        System.out.println("Illegal Access Exception: " + e.getMessage());
        System.exit(1);
    }
    return effect;
}
```

SpecialEffectInterface is the common interface used by all space effect classes, and is what this function returns. Let's take a look at this function in pieces.

```java
List<String> effectClasses = new ArrayList<String>();
```

First I set up a list to hold all the names of my special effect classes to be used later.

```java
File thisPath = new File(SpecialEffectInterface.class.getResource("SpecialEffectInterface.class").getPath());
```

Next I get the file path to where my effects are kept. Since all the effects are in the same directory as their common interface, I use that to find the path.

```java
String thisPackage = SpecialEffectInterface.class.getPackage().getName() + ".";
```

Then I get the package that they are all in. This is necessary later, as you'll see.

Now comes the fun part: generating a list of the effect classes. 

```java
File dir = new File(thisPath.getParent());
File[] children = dir.listFiles(new EffectFilter());
if (null != children) {
    for (int i=0; i<children.length; i++) {
        String filename = children[i].getName();
        effectClasses.add(thisPackage + filename.substring(0, filename.length()-6));
    }
}
```

This code creates a File object with the path we found to the effect classes, then creates a list of the items (children) in that directory given the `EffectFilter` class, which looks like this:

```java
package triangle_game.effects;

import java.io.*; 

public class EffectFilter implements FilenameFilter
{ 
    public boolean accept(File dir, String name)
    { 
        return name.endsWith("Effect.class");
    } 
}
```

This filter basically gives us everything in the directory that ends with "Effect.class" (for instance, NullEffect.class). So, as long as all effects are named "SomethingEffect" and are in the same directory as the interface, they will be found.

Continuing on, we then loop through the children, provided there are any. During this loop, we get the name of the files that matched our filter (the effect classes), then add the class name (without the .class extension) to our list of effect classes we created earlier. After all this, we now have a list of all the special effects we can use to assign to the board.

```java
int choice = 0 + (int)(Math.random() * (effectClasses.size() - 1));
String classChoice = effectClasses.get(choice);
SpecialEffectInterface effect = null;
try {
    effect = (SpecialEffectInterface) Class.forName(classChoice).newInstance();
} catch (ClassNotFoundException e) {
    System.out.println("Class Not Found: " + e.getMessage());
    System.exit(1);
} catch (InstantiationException e) {
    System.out.println("Instantiation Exception: " + e.getMessage());
    System.exit(1);
} catch (IllegalAccessException e) {
    System.out.println("Illegal Access Exception: " + e.getMessage());
    System.exit(1);
}
return effect;
```

Finally, we get a random number from 0 to one less than the size of the list. This number serves as the index of the list that will be the chosen effect. We get the effect name from the list, then in a fairly large try/catch block we get our random effect with a call to `Class.forName()` (which gives us the class object) followed by `.newInstance()` which actually returns the special effect object we need, which we then return from our function.

I'm sure there's a better way to do what I've done, but this is the way I figured out, and I'm pretty proud of it for now.

Anyway, I think I've come quite a long way in my development, and I've been trying to apply my new found knowledge of design patterns as I go. If you have any comments, concerns, or corrections, please feel free to comment.