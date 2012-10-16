---
layout: post
title: "Try and Variable Initialization"
date: 2012-08-21 21:55
comments: true
categories: 
- java
---
So, I learned a valuable lesson today that has taught me how to properly handle a particular error I kept getting when trying to compile some of my Java classes.
<!--more-->
Here is the basic offending code:

``` java
public class TryClass
{
    public static void main(String[] args)
    {
        String myString;
        try {
            myString = "ohai";
        } catch (Exception e) {
        }
        System.out.println(myString);
    }
}
```

The error the Java compiler gives is this:
    TryClass.java:10: variable myString might not have been initialized
            System.out.println(myString);
                               ^
For the life of me, I couldn't figure out the problem. Everything *looked* fine to me. Eventually, I realized that I could satiate the compiler by putting everything requiring the offending variable into the try block, like so:

``` java
public class TryClass
{
    public static void main(String[] args)
    {
        String myString;
        try {
            myString = "ohai";
            System.out.println(myString);
        } catch (Exception e) {
        }
    }
}
```

That allows the code to compile and run just fine. For this small test case its not an issue, but for a much larger method where the variable is used throughout, this just isn't a practical solution.
{% pullquote %}
Enter our old friend Google. I did a little searching and relearned something I'd forgotten in my years of writing loosely typed PHP: {" *declaring* a variable is not the same as *initializing* a variable "}. Once I remembered that, with some help from Google searches, I found my solution:
{% endpullquote %}

``` java
public class TryClass
{
    public static void main(String[] args)
    {
        String myString = null;
        try {
            myString = "ohai";
        } catch (Exception e) {
        }
        System.out.println(myString);
    }
}
```

Notice that I set the variable to null (in this case) prior to the try block, thus initializing (not just declaring) it so that the compiler knows it will always have a value. This really is one of those "God I feel so stupid right now" moments, but its just part of my adjustment from loosely-typed PHP to staticly-typed Java. There's certainly less room for mistakes, and I definitely like that.