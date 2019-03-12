---
title: "Design Patterns: Bridge Pattern"
date: 2013-08-02
categories: [blog]
tags: 
---
I recently have been (re)learning about design patterns and had an assignment of looking into the Bridge Pattern. In fact, part of the assignment was coming up with a good way of describing the pattern. I believe I have done this and felt like I should post my findings here, if only for my future self.
<!--more-->
One particular "textbook definition" of the Bridge Pattern (from [SourceMaking](http://sourcemaking.com/design_patterns/bridge)) is as follows:

"Decouple an abstraction from its implementation so that the two can vary independently."

If you're like me, you'll read this and go "huh?", then proceed to stare blankly at the words looking for some meaning. While that SourceMaking page does a good job of explaining what Bridge Pattern is on a technical level, what I needed was a dumbed-down explanation and example.

An Internet search for "what is the point of the bridge pattern" brought me to such an explanation. It can be found [here](http://softwarejedi.wordpress.com/2013/04/16/design-patterns-and-scala-the-bridge-pattern/), and I highly recommend reading it (but not just yet).


Let's say you have a program that deals with different beverages. There can be different be types of beverages (soda, beer, water, etc), and each can be contained within different types of containers (aluminum can, plastic bottle, glass bottle, etc). As you can see, we have two dimensions of "things": types of beverages and types of containers. Think of these as lists, and any item in one list can be paired with any item in another list. E.g. there can be canned beer, bottled beer, canned soda, bottled soda, etc.

So, let's say the containers are interfaces and the beverages are classes (implementations). In order to have all possible combinations of beverages and containers, we could manually pair them up and make the following classes:

```java
public class BottleSoda implements BottleInterface
{
  // do soda stuff
}

public class CanSoda implements CanInterface
{
  // do soda stuff
}

public class BottleBeer implements BottleInterface
{
  // do beer stuff
}

public class CanBeer implements CanInterface
{
  // do beer stuff
}
```

Hopefully you can see how quickly this can get really nasty. In this example, we're only dealing with a 2x2 matrix: two containers (bottle and can) and two drinks (beer and soda). If we needed to add, say, water, we would have to add two new classes:

```java
public class BottleWater implements BottleInterface
{
  // do water stuff
}

public class CanWater implements CanInterface
{
  // do water stuff
}
```

Then if we wanted to add glass bottles, we'd have to add three more:

```java
public class GlassSoda implements GlassInterface
{
  // do soda stuff
}

public class GlassBeer implements GlassInterface
{
  // do beer stuff
}

public class GlassWater implements GlassInterface
{
  // do water stuff
}
```

Like I said, it gets nasty really quick. We just went from 4 concrete classes to 9 just to add two things (the glass interface and the water implementation). On top of that, we have quite a bit of duplicate code. See all the comments like ```// do water stuff```?

So here's where the Bridge Pattern comes into play. Let's use our original 2x2 example. First, we want to be able to treat every type of container the same (for polymorphism purposes, etc.) as well as have common functionality (like having a contained beverage):

```java
public abstract class Container {
  private Beverage beverage;
  public Container (Beverage beverage) {
    this.beverage = beverage;
  }
  public abstract void fill();
}
```

Then we create individual classes for each of our containers, extending Container:

```java
public class Can extends Container {
  public void fill() {
    // fill with beverage
    // seal the can
  }
}

public class PlasticBottle extends Container {
  public void fill() {
    // fill with beverage
    // screw on the bottle cap
  }
}
```

So now we have two Containers that will hold beverages, no matter what the beverage actually is. We've abstracted out the beverages, but we still need write them. We start with a common interface (which was used in our classes above):

```java
public interface Beverage {
  public boolean alcoholic();
}
```

then the classes:

```java
public class Soda implements Beverage {
  public boolean alcoholic() {
    return false;
  }
}

public class Beer implements Beverage {
  public boolean alcoholic() {
    return true;
  }
}
```

Great! Now we have completely independent containers and beverages (although the containers do have a dependency on Beverage). How do we use it? Easy!

```java
Container cannedBeer = new Can(new Beer());
```

What if we want a plastic bottle of beer or soda instead?

```java
Container plasticBottledBeer = new PlasticBottle(new Beer());
Container plasticBottledSoda = new PlasticBottle(new Soda());
```

Now comes the real fruit of your labor. Remember how before, when we added water, we had to add two classes? Well now we just have to add one!

```java
public class Water implements Beverage {
  public boolean alcoholic() {
    return false;
  }
}
```

Then we can get either a can or a plastic bottle of water:

```java
Container cannedWater = new Can(new Water());
Container plasticBottledWater = new PlasticBottle(new Water());
```

Previously at this point, in order to add glass bottles for every type of beverage, we had to add three more classes. Now, we only have to add a single new class.

```java
public class GlassBottle extends Container {
  public void fill() {
    // fill the glass bottle with beverage
    // cap the bottle
  }
}
```

Getting a glass bottle of beer is no different than the others:

```java
Container glassBottledBeer = new GlassBottle(new Beer());
```

In total we now have the same functionality with 6 classes instead of 9 (if you don't include the abstract class), and we only ever have to add a single class any time we add an item to either group (beverage or container).

Hopefully this clears it all up for you. Now that you're through with my post, I recommend you finally go read the [article I referenced before](http://softwarejedi.wordpress.com/2013/04/16/design-patterns-and-scala-the-bridge-pattern/).
