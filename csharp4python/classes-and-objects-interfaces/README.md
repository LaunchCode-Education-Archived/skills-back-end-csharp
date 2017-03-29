---
title: 'Classes and Objects: Interfaces and Polymorphism'
currentMenu: csharp4python
---

The third and last **Pillar of Object-Oriented Programming** that we'll explore is **polymorphism**.

## Polymorphism

From our [glossary](../../glossary/):

<aside class="aside-definition" markdown="1">
**polymorphism**: An object-oriented mechanism that allows for objects of different types to be used in the same way.
</aside>

We've already encountered polymorphism made possible by inheritance. Recall the example from the [lesson on inheritance](http://localhost:8000/csharp4python/classes-and-objects-inheritance/#inheritance-in-c35) where we defined a `Cat` class, with subclasses `HouseCat` and `Tiger`.

Suppose we had a `CatOwner` like below.

```csharp
public class CatOwner
{
    public Cat Pet { get; set; }

    public  void FeedTheCat() {

        // ...code to prepare the cat's meal...

        Pet.Eat();
    }
}
```

The method `FeedTheCat` uses the property `Pet`, which is  of type `Cat`, but since a `HouseCat` *is a* `Cat` via inheritance, it is perfectly acceptable to use an instance of `HouseCat` to fill the `Pet` property.

```csharp
HouseCat suki = new HouseCat("Suki", 12);
CatOwner Annie = new CatOwner {
    Pet = suki
};

Annie.FeedTheCat();
```

Similarly, `FeedTheCat` can accept `Tiger` instances as well. This is because the only thing that the method requires is that the input parameter has the methods defined within `Cat`, and via inheritance, both of the subclasses satisfy this requirement. This is an example of polymorphism.

There's one more object-oriented mechanism that empowers us to code in a polymorphic way: the interface.


### Interfaces

An **interface** is a formal construction within C# that allows us to create a contract consisting of properties and method signatures (and a few other member types that we haven't covered). An interface *contains not method implementations*. In other words, we may not create a fully-functioning method within an interface.

Here's a simple example:

```csharp
public interface IFeedable
{

    void Eat();

}
```

And here are some observations:

- An interface is defined similarly to an abstract class, using the keyword `interface`. (We'll discuss similarities and differences between interfaces and abstract classes below.)
- `Eat` only has a signature. We are not allowed to provide a body for methods defined in interfaces.
- `Eat` does not have an access modifier. Interface members are always `public`. [Read about why this is the case.](http://stackoverflow.com/questions/6040785/why-do-interface-members-have-no-access-modifier).
- The interface itself is declared `public`, which means any other class may use it.
- The interface name begins with the letter `I` to make it clear to others using it that it is an interface type (more on using interfaces as types below). The rest of the name is indicative of the behavior that the interface is intended to describe. These are simply conventions, but every C# developer follows them, so you should too!

The purpose of an interface is to define a contract that classes may choose to uphold. In doing so, we say that they "implement the interface". The syntax for doing so is the same as for inheritance. Here's how we can use this interface in defining our `Cat` class.

```csharp
public class Cat : IFeedable
{

    public void Eat()
    {
        // method implementation
    }

    // ...rest of the class definition...

}
```

Since we've declared that `Cat` implements `IFeedable`, we have to provide an implementation for the `Eat` method, with signature as specified in the interface definition.

<aside class="aside-note" markdown="1">
You may extend a class and implement an interface at the same time, by separating the names with commas:
```csharp
public class MyClass : MySubclass, IMyInterface
{
    // ...code...
}
```
You should list the subclass before any interfaces.
</aside>

As with classes, interfaces define a type that can be used when declaring properties, fields, parameters, and local variables.

Using an interface allows us to relax the requirements on our code elsewhere, thus making it more extensible and adaptable. For example, here's how we might modify `PetOwner`:

```csharp
public class CatOwner
{
    public IFeedable Pet { get; set; }

    public  void FeedTheCat() {

        // ...code to prepare the cat's meal...

        Pet.Eat();
    }
}
```

Note that we've declared the property `Pet` to be of type `IFeedable`. This class assumes that the only behavior of `Pet` that we'll need within the class is the ability to `Eat`. But if that's all we need, then we should relax the requirements on the `Pet` property as much as possible. In fact, there's nothing specific about cats in this class, so we might make our code a step more abstract and flexible by doing the following:

```csharp
public class PetOwner
{
    public IFeedable Pet { get; set; }

    public  void FeedThePet() {

        // ...code to prepare the pet's meal...

        Pet.Eat();
    }
}

public class CatOwner : PetOwner
{
    // code that requires Cat-specific behavior
}
```

We've created a `PetOwner` class that encapsulates the behavior that could apply to any pet (any `IFeedable`, actually), and have `CatOwner` extend `PetOwner`. This allows other classes to extend `PetOwner` to make, say, a `DogOwner` that knows how to play fetch with their pet, or a `HorseOwner` that knows how to ride their pet. It also reduces the dependency of the `FeedThePet` method on the specific type of pet, since it doesn't need to care.

To use this new class design, we can look at the exact same sample code from above:

```csharp
HouseCat suki = new HouseCat("Suki", 12);
CatOwner Annie = new CatOwner {
    Pet = suki
};

Annie.FeedTheCat();
```

While the code usage here remains unchanged, the opportunities for using the classes we've built are much wider since the defined classes are no longer dependent on the specific `Cat` class. Also notice that we've used the object `suki` in a polymorphic way, creating it as a `HouseCat`, but using it as an `IFeedable` within the `CatOwner` class.

<aside class="aside-note" markdown="1">
Like inheritance, interfaces enable polymorphic usage of objects. We can create an object, and then use it in different contexts based on any interfaces that it implements.
</aside>

One final note before discussing how we might use interfaces in our code: *Interfaces may not be created like objects are, with* `new`. You may implement an interface, or declare variables and parameters as interface types. You can not, however, create an interface.

## Interfaces In The Wild

The most immediate situations that you'll encounter in which you'll want to use interfaces are when working with interfaces and classes that are part of C#. Here are just a few.

### IComparer&lt;T&gt;

**Purpose**: Compare two objects of a given class. This is a "parameterized" interface, which means that when using it you need to specify the class that it will be comparing. For example, `IComparer<Job>` would compare `Job` objects.

**Important Methods and Properties**: `Compare(T, T)`

[IComparer<T> Documentation](https://msdn.microsoft.com/en-us/library/system.collections.icomparer.compare(v=vs.110).aspx)

This interface can be used to determine, given two objects of the given type, which one is "greater" than the other. It is also used by collections such as [List<T>](https://msdn.microsoft.com/en-us/library/6sh2ey19(v=vs.110).aspx) to sort its contents with the [Sort](https://msdn.microsoft.com/en-us/library/234b841s(v=vs.110).aspx) method.

### IEnumerable<T>

**Purpose**: Enable iteration over a collection of objects using `foreach`.

**Important Methods and Properties**: `MoveNext()`, `Current`

[IEnumerable<T> Documentation](https://msdn.microsoft.com/en-us/library/9eekhta0(v=vs.110).aspx)

This interface is implemented by the `List<T>` class, which we've been using throughout this course.

### IList<T>

**Purpose**: Enable access to objects in a collection by index.

**Important Methods and Properties**: `Add(T)`, `Contains(T)`, `Remove(T)`, `Count`

[IList<T> Documentation](https://msdn.microsoft.com/en-us/library/5y536ey6(v=vs.110).aspx)

This interface is also implemented by the `List<T>` class, which we've been using throughout this course. In face, `IList<T>` extends `IEnumerable<T>`. An interface may extend another interface, in the same way that classes may extend each other.

### IDictionary

**Purpose**: Represent a collection of key/value pairs.

**Important Methods and Properties**: `Add(TKey, TValue)`, `Contains(T)`, `Remove(T)`, `Count`, `Keys`, `Values`

[IDictionary<TKey, TValue> Documentation](https://msdn.microsoft.com/en-us/library/s4ys34ea(v=vs.110).aspx)

This interface is implemented by the `Dictionary<TDey, TValue>` class, which we've been using throughout this course.

## Comparison to Abstract Classes

We mentioned above -- and you likely noticed yourself -- that interfaces share some characteristics with abstract classes. Recall that an abstract class is one declared with the `abstract` keyword. You may not create an abstract class, and like an interface, an abstract class is allowed to contain methods that only have signatures (that is, they don't have implementation code).

The main differences between interfaces and abstract classes are:
- You *implement* an interface, while you *extend* an abstract class. The net effect of this is that we can implement many interfaces while also extending a class.
- An abstract class may contain non-abstract methods. In other words, it may contain methods that have code. Interfaces may not.
- Abstract classes should be used to collect and specify behavior by related classes, while an interface should be used to specify related behaviors that may be common across unrelated classes.

For example, we could implement `IComparer` in many ways, to sort a wide variety of classes whose objects may be compared to one another: `Date` (compare by temporal order), `Student` (compare by GPA), `Person` (compare by age), `City` (compare by population). However, it's unlikely that these classes would have any implementable behavior that would warrant that they have the same base class.

## Benefits of Using Interfaces

Interfaces are great! Trust us, they really are. Once you get use to them, you'll begin to think more abstractly about which *behaviors* your code requires rather than which *classes* your code requires. This means you'll be able to code to interfaces instead of coding to classes, and your code will become more flexible and extensible.

Here are a few benefits of using interfaces:

- You can only extend one class, but you may implement many interfaces.
- You can extend a class and implement an interface at the same time.
- By declaring variables and parameters as interface types, you make your useful for a much wider variety of situations.
- When you declare properties and return types to be interface types, you decouple code using your classes from the actual class types you use. This means that you are free to change the specific implementation of your classes without affecting those using them. For example, if from a public method you returned an object of type `IEnumerable<Job>` then you would be free to change the method's internal structure to use, say, a [HashSet](https://msdn.microsoft.com/en-us/library/bb359438(v=vs.110).aspx) instead of a [List](https://msdn.microsoft.com/en-us/library/6sh2ey19(v=vs.110).aspx).

Remember that you don't need to start creating interfaces to use their power! When working with collections, in particular, think about the behaviors that your code requires, and declare variables and parameters to be interface types if you only need to use specific behaviors such as ordering or iteration.

## References

- [Interface Naming Guidelines (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/8bc1fexb(v=vs.71).aspx)
- [Interfaces (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ms173156.aspx)
- [IComparer<T> Interface](https://msdn.microsoft.com/en-us/library/8ehhxeaf(v=vs.110).aspx)
- [IEnumerable<T> Interface](https://msdn.microsoft.com/en-us/library/9eekhta0(v=vs.110).aspx)
- [IList<T> Interface](https://msdn.microsoft.com/en-us/library/5y536ey6(v=vs.110).aspx)
- [IDictionary<TKey, TValue> Interface](https://msdn.microsoft.com/en-us/library/s4ys34ea(v=vs.110).aspx)
