---
title: 'Classes and Objects: Encapsulating Data'
currentMenu: java4python
---

In this lesson we begin our discussion of encapsulation, focusing on data fields of classes.

## Encapsulation

From our [Glossary](../../glossary/), here's a definition of encapsulation:

<aside class="aside-definition" markdown="1">
**encapsulation:** The bundling of related data and behaviors that operate on that data, usually with restricted access to internal, non-public data and behaviors. In object-oriented programming, encapsulation is achieved through the use of objects.
</aside>

In other words, classes and objects allow us to encapsulate, or isolate, data and behavior to only the parts of our program to which they are relevant. And the concept of restricted access allows us to expose only that data and behavior that we want others to be able to use.

We'll introduce data-related concepts in this lesson by gradually building up an solid example of a class that represents a student, `Student`.

## Fields and Properties

We previously defined a **field** as a variable, or piece of data, that belongs to the class. For our `Student` class, let's think about the data that is typically associated with a student (in the sense of a high school or college student). There are a lot of possibilities, but here are probably the most important:

- Name
- Student ID
- Number of credits
- GPA

In order to declare these fields within our class, we'll need to determine the best data type for each. A field may be of any primitive or object type. In this case, the following types will work best:

- Name: `string`
- Student ID: `int`
- Number of credits: `int`
- GPA: `double`

Let's put these inside of a class. While they may be declared anywhere within a class, fields should always be declared at top of the class. When we're ready to add methods, we'll add them below.

```csharp
public class Student {

    string name;
    int studentId;
    int numberOfCredits;
    double gpa;

}
```

Like variables within a method, fields may be initialized when they are declared. For example, we could provide default values for `numberOfCredits` and `gpa` (default values for `name` and `studentId` don't make sense since they should be different for each student).

```csharp
int numberOfCredits = 0;
double gpa = 0;
```

Fields are also referred to as **instance variables**, since they belong to an instance of a class. In other words, each object will have its own copy of each instance variable.

### Properties and Accessor Methods

A **property** in C# is a mechanism to read, write, or compute the value of a private field.

As declared, our four fields are private, which means that they are inaccessible to code outside of the `Student` class. As a rule-of-thumb, direct access to fields by code outside classes you write should not be allowed. Understanding why this is the case is the goal of this section.

In order to provide access to private fields, **getter and setter methods** are used. Collectively, these methods are called **accessors**. Getters and setters do what you might guess: get and set a given field. If we make the getter and/or setter public for a given field, then others will be able to access it in that way. Collectively, a private field along with accessor methods make up a property.

Here is how we can expose `Name` via accessor methods (you can imagine how the others would be written).

```csharp
private string name;

public string Name
{
    get { return name; }
    set { name = value; }
}
```

Here, within `get` and `set`, `name` refers to the private field that stores the value of the property. In `set`, the special variable `value` will contain the value that the user is trying to set within the property.

We can then get or set the value of name anywhere else (since it's public) using dot-notation:

```csharp
Student josh = new Student();

// set the Name
josh.Name = "Josh";

// get the Name
Console.WriteLine(josh.Name);
```

When you use properties in this way, the get/set methods are called implicitly when assigning or reading the property, therefore parentheses are not needed.

An astute question to ask at this point would be, "Why make the fields private if you're just going to allow people to get and set them anyway!?" Great question. There are lots of reasons to use getters and setters to control access. Here are just a few:

1. Sometimes you'll want to implement behavior that happens every time a field is accessed (get) or changed (set). Even if you can't think of such a reason when writing your class, you might later have the need to add such behavior. If you don't use accessors, you'll have to do a lot more refactoring at that point.
2. You can perform validation within a setter. For example, we might want to ensure that a student's name contains only certain characters, or that their student ID is a positive integer.
3. You can use different access modifiers on getters and setters for the same field, based on desired usage. For example, you might want to allow anyone to be able to read the value of a field, but only classes within the same assembly to modify it. You could do this with a `public` getter and an `internal` setter, but not as a field without getters and setters, which could only be public to everyone or internal to everyone.

<aside class="aside-question" markdown="1">
One of the four fields in our `Student` class is a prime candidate for the scenario described in item 3. Which one do you think it is?
</aside>

To set different access levels on a property, use an access modifier next to `get` or `set`. Here's how we would make `Name` readable by everyone, but modifiable only by code within the class's assembly.

```csharp
private string name;

public string Name
{
    get { return name; }
    internal set { name = value; }
}
```

If a field has both a public getter and setter, and no additional logic is needed, we can use the shorthand:

```csharp
string Name { get; set; }
```

This is referred to as an **auto-implemented property**.

<aside class="aside-warning" markdown="1">
Note that in the example above the private field is `name` (lowercase) while the property is `Name`. The property is based on the value of the private field `name`, and since C# identifiers are case-sensitive, these are two distinct members. `name` is referred to as a "backing field", and it stores the value of the property.

If you were to try to use the same identifier for both the backing field and the property, you'll see a `StackOverflowException` due to infinite recursion -- i.e., the property would infinitely call itself!
</aside>

When using this syntax, the compiler will generate the following equivalent code for us. That is, the compiler generates code identical to the first example of accessors above.

As an example of validation within a setter, let's take a short detour to look at a `Temperature` class. A valid temperature can only be so low ("absolute zero"), so we wouldn't want to allow somebody to set an invalid value. In `set` we throw an exception if an invalid value is provided (we'll cover exceptions in detail later, but for now note that they are ways of signaling errors).

```csharp
public class Temperature {

    private double fahrenheit;

    public double Fahrenheit
    {
        get
        {
            return fahrenheit;
        }
        set
        {
            double absoluteZeroFahrenheit = -459.67;

            if (value < absoluteZeroFahrenheit) {
                throw new ArgumentException("Value is below absolute zero");
            }

            fahrenheit = value;
        }
    }
}
```

There's a nice detailed discussion that provides additional perspective on why to use getters and setters on [Stack Overflow](http://stackoverflow.com/questions/1568091/why-use-getters-and-setters) (the discussion here refers to Java, but the concepts apply to C# just the same).

Most often, properties will correspond directly to a private backing field, but they don't have to. Let's look at an example of a property that doesn't directly correspond to a field. If we wanted to add a `Celsius` property to the `Temperature` class above, we might do it as follows:

```csharp
public double Celsius
{
    get { return (Fahrenheit - 32) * 5.0 / 9.0; }
    set { Fahrenheit = value * 9.0 / 5.0 + 32; }
}
```

Since there's a link between Fahrenheit and Celsius, we want to make sure that when one is updated, so is the other. In this case, we only store one field value (`fahrenheit`, the backing field for `Fahrenheit`) and make the appropriate calculation when getting or setting the `Celsius` property. Using a property like this is the same as when there is a private field behind it; the code using it can't tell the difference.

### Readonly Fields

A **readonly field** is one that can not be changed once it is initialized (assigned a value). This means slightly different things for primitive and class types. We create readonly fields by declaring them with the `readonly` keyword.

**Readonly value-type fields** can not change their value once they are initialized.

**Readonly reference-type fields** may not change the object that they hold once they are initialized. However, that object itself my change.

Furthermore, **readonly fields may only be initialized when declared, or in a constructor.** Calling a constructor is what we are doing when creating a new object, as in `Student josh = new Student()`. We'll explore creating our own constructors in the next lesson.

Here are some examples to illustrate. Each class would be in its own file, but we present them side-by-side for convenience. Note that the first line of the `FortyTwo` class initializes the property at the point at which it is declared.

```csharp
public class FortyTwo
{
    public int intValue = 42;
}

public class ReadonlyFields {

    public readonly int intValue = 42;
    public readonly FortyTwo objectValue = new FortyTwo();

    public static void Main(string[] args)
    {

        ReadonlyFields demo = new ReadonlyFields();

        // This would result in a compiler error
        demo.intValue = 6;

        // This would result in a compiler error, since we're
        // trying to give objectValue a different object value
        demo.objectValue = new FortyTwo();

        // However, this is allowed since we're changing a field
        // inside the readonly object, and not changing which object
        // objectValue refers to
        demo.objectValue.intValue = 6;
    }
}
```

Note that `readonly` doesn't make much sense for properties, and in fact may not be applied to properties.

### Static Fields and Properties

A **static** field or property is one that is declared with the `static` keyword. We have encountered the `static` keyword used with both fields and methods, but since this discussion is focused on data, let's only discuss static fields and properties for now.

A static member is shared by all instances of the class. For example, in our `Temperature` class there is no good reason that each `Temperature` object needs its own instance property `double absoluteZeroFahrenheit`, since that value will not vary from class to class. Let's make it a static field. After doing so, there will be a single field `absoluteZeroFahrenheit` that is shared among *all* instances of the `Temperature` class.

```csharp
public class Temperature {

    private static double absoluteZeroFahrenheit = -459.67;

    private double fahrenheit;

    public double Fahrenheit
    {
        get
        {
            return fahrenheit;
        }
        set
        {

            if (value < absoluteZeroFahrenheit) {
                throw new ArgumentException("Value is below absolute zero");
            }

            fahrenheit = value;
        }
    }

}
```

Within the class, we can refer to the static field or property the same way as a non-static field or property. For example, within `Temperature` we could write:

```csharp
Console.WriteLine("Absolute zero in F is: " + absoluteZeroFahrenheit);
```

Outside the class, we must use the class name to refer to the field (since it doesn't belong to any one instance/object).

```csharp
Console.WriteLine("Absolute zero in F is: " + Temperature.absoluteZeroFahrenheit);
```

### Constants

C# allows us to create constants -- named values that may not be changed -- using the keyword `const`.

```csharp
public class Constants {
    public const double PI = 3.14159;
    public const String FIRST_PRESIDENT = "George Washington";
}
```

There are a couple of notable things in this example:
- We use a different naming convention for constants than for other variables. Constants should be in all-caps, with an underscore to separate words.
- Since constants can't be modified by any code -- including the class that contains them -- it's safe to make them public fields if they're meant to be used broadly. That is, there isn't a good reason to make them properties. Of course, if a constant should only be used by the class it is declared in, it should still be private.

<aside class="aside-pro-tip" markdown="1">
You may also use the `const` modifier with local variables.
</aside>

A good use of a constant can be seen in our `Temperature` class. Since absolute zero will never change, we can ensure that nobody ever changes it (perhaps by mistake, even) by adding `const` to make it a constant.

```csharp
public class Temperature {

    public const double ABSOLUTE_ZERO_FAHRENHEIT = -459.67;

    /* Rest of class, as above... */

}
```

Applying the proper modifiers to fields and properties -- access modifiers, `static`, `readonly`, and `const` -- is part of proper encapsulation. C# has much more machinery to allow you as the programmer to control how the code you write is used, which can minimize bugs and increase stability and modularity of your code, if you use them properly.

## References

- [Encapsulation (wikipedia.org)](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming))
- [Properties in C# (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/x9fsa0sw.aspx)
- [Auto-Implemented Properties (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/bb384054.aspx)
- [Restricting Accessor Accessibility in C# (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/75e8y5dd.aspx)
- [static (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/98f28cdx.aspx)
- [const (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/e6w8fe1b.aspx)
- [readonly (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/acdd6hb7.aspx)
