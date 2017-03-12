---
title: 'Classes and Objects: Inheritance'
currentMenu: csharp4python
---

Inheritance is the second of the **Three Pillars of Object-Oriented Programming** that we will encounter.

From our [Glossary](../../glossary/), here's a definition:

<aside class="aside-definition" markdown="1">
**inheritance**: A mechanism within object-oriented programming that allows one class to be based on another class, thus "inheriting" its properties and behaviors. Inheritance is also sometimes referred to as **subtyping**.
</aside>

## Inheritance in C&#35;

Inheritance in C# is very similar to the same concept in Python. We **extend** another class to inherit its data and behaviors (that is, fields, properties, and methods). Recall that in Python the syntax for inheritance was the following:

```python
class Cat:
    # ...code for the Cat class...

class HouseCat(Cat):
    # ...code for the HouseCat class...
```

Any fields and non-constructor methods in `Cat` would be available to each instance of `HouseCat`. We express the inheritance relationship in plain English by saying that a `HouseCat` *extends* `Cat`, or that a `HouseCat` *is a* `Cat`.

In C#, the syntax for extending a class requires a colon (`:`) separating the two class names.

```csharp
public class Cat
{
    // ...code for the Cat class...
}

public class HouseCat : Cat
{
    // ...code for the HouseCat class...
}
```

We say that `HouseCat` is a **subclass**, **derived class**, or **child class** of `Cat`, and we say that `Cat` is the **superclass**, **base class**, or **parent class** of `HouseCat`. In C#, a class may extend only one class, but classes may extend each other in turn, creating hierarchies of classes. We often visualize these by drawing each class as a box, with lines descending from the base class to the subclass.

![Inheritance Diagram](inheritance.png)

Inheritance is a useful mechanism for sharing data and behavior between related classes, and it effectively creates hierarchies of classes that have more and more specialized behavior as you go from base class to subclass.

As with Python, fields and non-constructor methods are directly available within the subclass, and may be called as if the belonged to the base class, subject to any access modifiers. In general, this means that `private` and `internal` members of a base class are not accessible to a subclass. (However, if the subclass and class are in the same assembly, `internal` would allow access to a member.)

<aside class="aside-note" markdown="1">
This is a good time to review [access modifiers in C#](../introduction-to-classes-and-objects/#access-modifiers) if anything in the last paragraph was fuzzy.
</aside>

For an example, let's revisit our `Cat` and `HouseCat` implementations from [Chapter 14 of Unit 1](https://runestone.launchcode.org/runestone/static/thinkcspy/ClassesDiggingDeeper/Inheritance.html), modified to illustrate some C#-specific concepts.

```csharp
public class Cat {

    public bool IsTired { get; set; } = false;
    public bool IsHungry { get; set; } = false;
    public double Weight { get; set; }

    // The biological Family for all cat species
    private string family = "Felidae";
    public string Family
    {
        get { return family; }
        private set { family = value; }
    }

    public Cat (double weight) {
        Weight = weight;
    }

    // A cat is rested and hungry after it sleeps
    public void Sleep()
    {
        IsTired = false;
        IsHungry = true;
    }

    // Eating makes a cat not hungry
    public void Eat()
    {

        // eating when not hungry makes a cat sleepy
        if (!IsHungry)
        {
            IsTired = true;
        }

        IsHungry = false;
    }

    public virtual void Noise ()
    {
        Console.WriteLine("Meeeeeeooooowww!");
    }
}
```

```csharp
public class HouseCat : Cat
{
    public string Name { get; set; }

    private string species = "Felis catus";
    public string Species
    {
        get { return species; }
        private set { species = value; }
    }

    public HouseCat(string name, double weight) : base(weight)
    {
        Name = name;
    }

    private bool IsSatisfied()
    {
        return !IsHungry && !IsTired;
    }

    public override void Noise()
    {
        if (IsSatisfied())
        {
            Console.WriteLine("Hello, my name is " + Name + "!");
        }
        else
        {
            base.Noise();
        }
    }

    public void Purr()
    {
        Console.WriteLine("I'm a HouseCat");
    }
}
```

The class `HouseCat` extends `Cat`, using several different inheritance features that we will explore in turn.

Notice that `Cat` has a private string property `family`, representing the biological family of all cats. This property is not directly accessible to `HouseCat` since it is private, however it may be read via the property `Family`. The setter for `Family` is private, however, so it may only be set within `Cat`.

Methods of the base class may be called on instances of the subclass as if they were defined as part of the subclass.

```csharp
HouseCat garfield = new HouseCat("Garfield", 12);
garfield.Eat();
```

The `Eat` method was defined in `Cat`, but may be called on all `HouseCat` instances as well. We say: "`HouseCat` inherits the method `Eat` from `Cat`."

### Working With Constructors in Subclasses

We mentioned above that a subclass inherits all non-constructor methods. Indeed, when extending a class, we will not be able to create new instances of our subclass `HouseCat` using the constructor provided by `Cat`. For example, this code will not compile:

```csharp
HouseCat thumper = new HouseCat(8.4);
```

The base class `Cat` has a constructor that takes a single parameter of type `double`, but `Cat` constructors are not inherited by `HouseCat`. If we wanted to use such a constructor in the subclass, we would have to explicitly provide it. We'll see how to do this relativel easily in a bit.

Let's look at the constructor included in `HouseCat`:

```csharp
public HouseCat(string name, double weight) : base(weight)
{
    Name = name;
}
```

Here we use the `:` operator in conjunction with they keyword `base` to specify that our constructor should call the base class constructor with the argument `weight`. This call to the base class constructor will run before the body of the subclass constructor executes. This is a useful way to ensure that we're fully initializing our objects.

You may leave out such a call to a base class constructor only when the base class has a default, or no-arg, constructor (that is, a constructor that takes no arguments). In such a case, the default constructor is implicitly called for you. Here's what this would look like in `HouseCat`, if `Cat` had a default constructor.

```csharp
public HouseCat(string name)
{
    Name = name;
}
```

As a consequence of this constructor syntax, we can easily "expose" any constructor from the base class by providing a subclass constructor with the same signature and no body, and calling the base class constructor.

```csharp
public HouseCat(double weight) : base(weight) {}
```

<aside class="aside-warning" markdown="1">
This constructor is a bad one, and is included merely to introduce syntax and usage. We would not want to have a constructor for `HouseCat` that didn't initialize an essential property such as `Name`.
</aside>

### Overriding Base Class Behavior

Sometimes when extending a class, we'll want to modify behavior provided by the base class. We can do this via **method overriding**, if the base class allows.

For a method in a base class to be overridden in a subclass, it must be marked as `virtual`. In our example, the `Noise` method of `Cat` is marked `virtual`, which means we may override it in `HouseCat`. When we override it, we must use the `override` keyword.

<aside class="aside-warning" markdown="1">
Unlike in some other object-oriented languages (notably Java), in C# a method must explicitly allow itself to be overridden by using the `virtual` keyword.
</aside>

Here are the methods in question, pulled out for convenience.

In `Cat`:

```csharp
public virtual void Noise()
{
    Console.WriteLine("Meeeeeeooooowww!");
}
```

In `HouseCat`:

```csharp
public override void Noise()
{
    Console.WriteLine("Hello, my name is " + Name + "!");
}
```

Here we override `Noise` in `HouseCat`. If we have a `HouseCat` object and call it's noise method, we will be using the method defined in `HouseCat`.

```csharp
Cat plainCat = new Cat(8.6);
HouseCat garfield = new HouseCat("Garfield", 12);

plainCat.Noise(); // prints "Meeeeeeooooowww!"
garfield.Noise(); // prints "Hello, my name is Garfield!"
```

When overriding a method, we may call the method that we're overriding by using `base`:

```csharp
public override void Noise()
{
    if (IsSatisfied())
    {
        Console.WriteLine("Hello, my name is " + Name + "!");
    }
    else
    {
        base.Noise();
    }
}
```

Notice the method call: `base.Noise()`. This calls the overridden method in the base class, carrying out the original behavior if the given conditional branch is reached.

### The Object Class

In a previous lesson, we introduced the "special" methods `Equals` and `ToString`, noting that all classes were provided default implementations of these methods that could be overridden.

In fact, these default methods are part of a class called `Object`. If a class does not explicitly extend another class, then it implicitly extends `Object`. So the default implementations of `Equals` and `ToString` (along with a few [other methods](https://msdn.microsoft.com/en-us/library/system.object(v=vs.110).aspx#Methods)) are made available to us via inheritance. Those that are marked `virtual` -- such as `Equals` and `ToString` both are -- may be overridden.

### Abstract Classes and Class Members

In this section we briefly introduce an intermediate object-oriented concept. We will not use it much in this course, but you're likely to encounter it in the "real world" and it is a useful one to know.

We noted in the introduction to this section that inheritance is a way to share behaviors among classes. You'll sometimes find yourself creating a base class as a way to share behaviors among related classes. However, in such situations is not always desirable for instances of the base class to be created.

For example, suppose we began coding two classes, `HouseCat` and `Tiger`. Upon writing the code, we realized that there were some common data and behaviors, and so to reduce code repetition, we combined those in `Cat` (as above).

```csharp
public class Cat
{
    // Cat class definition
}

public class HouseCat : Cat
{
    // HouseCat class definition
}

public class Tiger : Cat
{
    // Tiger class definition
}
```

In reality, though, we might not want objects of type `Cat` to be created, since such a cat couldn't actually exist (a real cat would have a specific genus and species). We could prevent objects of type `Cat` from being created, while still enabling sharing of behavior among its subclasses, by making `Cat` and **abstract class**.

```csharp
public abstract class Cat
{
    // Cat class definition
}
```

To reiterate, abstract classes are classes that may not be instantiated. In order to use the behavior of an abstract class, *we must extend it*.

We have a further tool that we may use here, which is an **abstract method**. An abstract method is a method in an abstract class that does not have a body. In other words, it does not have any associated code, only a signature. It must also be marked `abstract`.

In our abstract `Cat` class, it would make sense to make `Noise` abstract to force any class extending it to provide its own implementation of that behavior.

```csharp
public abstract class Cat
{
    public abstract void Noise();

    // Additional Cat class definition
}
```

Any class extending `Cat` is then forced to provide its own version of `Noise`, with the exact same method signature.

## References

- [Inheritance in C# (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ms173149.aspx)
- [The override keyword (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ebca9ah3.aspx)
- [The virtual keyword (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/9fkccyh4.aspx)
- [The Object Class (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/system.object(v=vs.110).aspx)
- [Abstract Classes and Class Members](https://msdn.microsoft.com/en-us/library/ms173150.aspx)
