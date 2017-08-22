---
title: 'Classes and Objects: Encapsulating Behavior'
currentMenu: java4python
---

Having explored configuring data within classes (via fields and properties), let's turn our attention to configuring behavior (methods).

## Calling Methods on Objects

A **method** is a procedure that belongs to a class. In C# all procedures must be part of a class, which is a significant difference from Python where functions may stand on their own. Let's revisit our minimal class example.


```csharp
public class HelloWorld {

    private string message = "Hello World";

    public void SayHello() {
        Console.WriteLine(message);
    }

}
```

There is one method in this class, `SayHello`. In order to call this method, we must have an object created from the `HelloWorld` class template. In other words, we must have an instance of `HelloWorld`.

Here's how you call methods on an object.

```csharp
HelloWorld hello = new HelloWorld();
hello.SayHello();
```

It is not possible to call `SayHello` without having a `HelloWorld` object. This begins to make more sense when you note that the `message` field is used within `SayHello`, and unless we are calling `SayHello` off of an object, there will be no `message` field available to print.

<aside class="aside-pro-tip" markdown="1">
As mentioned before with fields, methods should also have the most restrictive level of access possible. If you create a utility method that should only be used within your class, then it should be `private`.

Only make methods `public` when you expect other classes to use them, and when you are committed to maintaining those methods for other programmers that might use them.
</aside>

## Instance Methods

So far we've only looked at examples of methods that are relatively specialized: constructors, getters, and setters. Virtually every class you create will have these methods. What will make your classes different from each other, and effective, are the specific behaviors that are unique to your classes.

Let's add a couple of such methods to our `Student` class. These methods will be **instance methods** since they will belong to each `Student` object created, and will use the data of each such object.

What are the behaviors that our `Student` class should have? To start, it would make sense for a student to take a class and get a grade, and for their data to be updated accordingly. Additionally, it would be nice to be able to easily tell the grade level of a student - freshman, sophomore, junior, or senior.

For our last look at the `Student` class we will stub out these methods below, without providing the implementation. That job is left to you to do as an exercise.

```csharp
public class Student
{

    private static int nextStudentId = 1;
    public string Name { get; set; }
    public int StudentId { get; set; }
    public int NumberOfCredits { get; set; }
    public double Gpa { get; set; }

    public Student(string name, int studentId,
            int numberOfCredits, double gpa)
    {
        Name = name;
        StudentId = studentId;
        NumberOfCredits = numberOfCredits;
        Gpa = gpa;
    }

    public Student(string name, int studentId)
        : this(name, studentId, 0, 0) {}

    public Student(string name)
        : this(name, nextStudentId)
    {
        nextStudentId++;
    }

    public void AddGrade(int courseCredits, double grade)
    {
        // Update the appropriate properties: NumberOfCredits, Gpa
    }

    public string GetGradeLevel()
    {
        // Determine the grade level of the student based on NumberOfCredits
    }

}
```

When creating your classes, think about the behaviors that you want to make available, as well as the access level of those methods.

## Static Methods

Static methods are not new to us. We've used them quite a bit, all the way back to our first C# method: `public static void main(string[] args)`. Now let's present them in the context of the rest of what we've recently learned about classes.

Analogous to static fields, **static methods** belong to a class, and not to any of the objects created by the class. Thus, they are sometimes also called **class methods**.  A static method can be thought of as the opposite of an instance method, since the two cases are mutually exclusive; one relies on data from an object (instance methods) while the other must *not* rely on data from an object (static methods).

A static method may be called by preceding it with the class name and using dot-notation. Here's an example that we looked at previously.

```csharp
public class HelloMethods
{

    public static void Main(string[] args)
    {
        string message = Message.GetMessage("fr");
        Console.WriteLine(message);
    }

}
```

```csharp
public class Message {

    public static string GetMessage(string lang)
    {

        if (lang.equals("sp"))
        {
            return "Hola Mundo";
        }
        else if (lang.equals("fr"))
        {
            return "Bonjour le monde";
        }
        else
        {
            return "Hello World";
        }
    }
}
```

The call in question is: `Message.GetMessage("fr")`. We call the static method `GetMessage` without needing an instance of the `Message` class, using the name of the class itself.

<aside class="aside-warning" markdown="1">
It is technically allowed to call a static method using an instance of a class: `myObject.SomeStaticMethod()`. However, this should be avoided in favor of using the class name to call the method.
</aside>

A method should be static when it does not refer to any instance fields of the containing class (it *may* refer to static fields, however). These methods tend to be utility-like, carrying out a calculation, or using or fetching some external resource.

## Special Methods

Every class has a few special methods that belong to it, regardless of whether or not we define them. Exactly how every class obtains these methods will be explored in a future lesson. For now, let's look at the most important of these methods.

### ToString

The `ToString` method returns a string representation of a class. Calling `ToString` on a class that you've written will result in something like this:

```nohighlight
School.Student
```

Here, we called `ToString` on a `Student` object. Generally, the default `ToString` implementation is not very useful, and you'll want to override it. You can write your own `ToString`. Here's how we might do it for `Student`:

```csharp
public override String ToString()
{
    return Name + " (Credits: " + NumberOfCredits + ", GPA: " + Gpa + ")";
}
```

This would result in a much more friendly message:

```nohighlight
John (Credits: 0, GPA: 0.0)
```

In the definition of `ToString` we are required to use a new keyword, `override`. This is a flag to the compiler that the method is meant to override the default `ToString` behavior.

Note that `ToString` is often implicitly called for you. For example, the output above could have been generated by the following code, which implicitly calls `ToString` on `john` within `Console.WriteLine`.

```csharp
Student john = new Student("John");
Console.WriteLine(john);
```

### Equals

Suppose we had two objects of type `Student`, say `student1` and `student2`, and we wanted to determine if they were equal. We might try to compare them using `==`, but since these are [references](../data-types#reference-and-value-types) -- that is, the variables hold a reference, or the address of the actual `Student` objects -- they will be determined to be equal only when they have the same address. In other words, they will be equal only when they refer to, or point at, the exact same object. This is often not what we want to check for. For example, we might want to consider two student objects equal if they had the same name, email, or student ID.

The `Equals()` method can be used to determine if one object is equal to another in this sense. We introduced this method when discussing strings, but it also applies to all other classes. Here's now you might use it:

```csharp
Student bono1 = new Student("Paul David Hewson", 4);
Student bono2 = new Student("Bono", 4);

if (bono1.Equals(bono2))
{
    Console.WriteLine(bono1.getName() +
        " is the same as " + bono2.getName());
}
```

If we don't provide our own `Equals()` method, then the one provided for us will only consider two objects equal if they are the *exact same object*. In other words, they will only be considered equal if the variables referring to the given objects both point at the same object. This is the same behavior that we would see when using the `==` operator: `bono1 == bono2`. This expression will evaluate to true only if the variables actually refer to the same object.

This is often not what we want. The difference between the comparison carried out by the default `Equals()` method and the `==` operator, and how we would like our classes to behave, is the difference between *equality* and *identity*. Two things can be considered equal even if they are not the exact same item, that is, even if they are not identical.

In the case of the `Student` class, we might specify that two `Student` objects are equal if they have the same ID:

```csharp
public override bool Equals(Object o)
{
    Student studentObj = o as Student;
    return StudentId == studentObj.StudentId;
}
```

One catch of working with `Equals()` is that its input parameter must be of type `Object`, even if we're working in a class like `Student`. The reason why will become more clear in the next lesson, where we introduce the `Object` class. For now, the practical implication is that we must convert, or **cast**, the input `o` to be of type `Student` with the syntax `Student studentObj = o as Student`. Then we compare the converted student's ID to that of the current student.

Here's what this looks like conceptually:

**Equality**

![Equality](equality.png)

**Identity**

![Identity](identity.png)

You'll often want to implement `Equals()` yourself. However, if you do so, be sure to understand best practices around how the method should behave, which are [not so simple][implementing-equals]. In fact, the `Equals()` method we have here isn't very good by most C# programmers' standards. Let's improve on it.

**Problem #1**: The method argument can not be converted to a `Student` instance.

When we attempt to cast the argument `o` to type `Student`, we'll get an exception if `o` can't be properly converted. This would happen if somebody passes something other than a `Student` object into `Equals()`. To prevent this from happening, we'll return `false` if `o` was not created from the `Student` class, as determined by using the `GetType` method, which is available to every object (similarly to `ToString`).

```csharp
public bool Equals(Object o)
{

    if (o.GetType() != GetType())
    {
        return false;
    }

    Student studentObj = o as Student;
    return StudentId == studentObj.StudentId;
}
```

This check ensures that the two objects that we want to compare were created from the same class.

**Problem #2:** `o` might be `null`.

If `o` is `null` then `o.GetType()` will result in an exception. This is an easy issue to fix, since comparing a non-null object to `null` will evaluate to `false`. Therefore, if this comparison evaluates to true then we know that the object is null and `Equals()` should return `false`.

```csharp
public bool Equals(Object o)
{

    if (o == null)
    {
        return false;
    }

    if (o.GetType() != GetType())
    {
        return false;
    }

    Student studentObj = o as Student;
    return StudentId == studentObj.StudentId;
}
```

**Problem #3:** The two objects to compare are _the same_ object.

This is less of a problem per se and more of a way we can improve our `Equals()` method. If `o` is the same literal object that we are attempting to compare it to, then we can make a quick determination and save a few checks.

```csharp
public bool Equals(Object o)
{

    if (o == this)
    {
        return true;
    }

    if (o == null)
    {
        return false;
    }

    if (o.GetType() != GetType())
    {
        return false;
    }

    Student studentObj = o as Student;
    return StudentId == studentObj.StudentId;
}
```

#### Components of Equals

Almost every equals method that you write will look similar to this one, and will contain the following segments, in order:

1. **Reference check:** If the two objects are the same, return `true` right away.
1. **Null check:** If the argument is `null`, return `false`.
1. **Class check:** Compare the classes of the two objects to ensure a safe cast.
1. **Cast:** Convert the argument to the type of our class, so getters and other methods can be called.
1. **Custom comparison:** Use custom logic to determine whether or not the two objects should be considered equal. This will usually be a comparison of properties or fields.

#### Characteristics of Equals

Now that we know how to write an `Equals()` method, let's look at some characteristics that every such method should have. If you follow the general outline above, ensuring that your `Equals()` method has these characteristics should be straightforward.

1. **Reflexivity:** For any non-null reference value `x`, `x.Equals(x)` should return `true`.
1. **Symmetry:** For any non-null reference values `x` and `y`, `x.Equals(y)` should return `true` if and only if `y.Equals(x)` returns true.
1. **Transitivity:** For any non-null reference values `x`, `y`, and `z`, if `x.Equals(y)` returns `true` and `y.Equals(z)` returns `true`, then `x.Equals(z)` should return `true`.
1. **Consistency:** As long as `x` and `y` do not change `x.Equals(y)` should always return the same result.
1. **Non-null:** For any non-null reference value `x`, `x.Equals(null)` should return `false`.

If you think about your general sense of the concept of equality, say, from a math class, then these concepts make sense. While using the general approach outlined above for implementing `Equals()` will generally make these relatively simple to guarantee, not guaranteeing these characteristics can be disastrous for your C# applications.

### GetHashCode

Seasoned C# developers will tell you that every time you implement your own version of `Equals()` you should also implement your own version of `GetHashCode()`. `GetHashCode()` is another special method that every class has. It is called on an object to return an integer, called a **hash code**, and is used frequently by the built-in data structures in C#.

The main rules that you should follow with `GetHashCode` are:
- Always provide a custom `GetHashCode` implementation whenever you provide a custom `Equals` implementation
- When two objects are equal, as determined by `Equals`, then they should have the same hash code, as determined by `GetHashCode`.

One simple case is when we build our class to use unique IDs, as is the case with our `Student` class. In that case, we have `Equals` make its comparison using this ID, and we can have `GetHashCode` return the integer ID of the given object.

```csharp
public override bool Equals(Object o)
{
    if (o == this)
    {
        return true;
    }

    if (o == null) || o.GetType() != GetType())
    {
        return false;
    }

    Student studentObj = o as Student;
    return StudentId == studentObj.StudentId;
}

public override int GetHashCode()
{
    return StudentId;
}
```

You can check that these methods satisfy the rules discussed above.

Understanding `GetHashCode()` in full detail would take us a bit far afield at this point, but we would be remiss to not mention it. If you want to read more, [go for it](https://docs.microsoft.com/en-us/dotnet/api/System.Object.GetHashCode?view=netcore-1.0)!

<aside class="aside-pro-tip" markdown="1">
Visual Studio can generate an outline of the `Equals` and `GetHashCode` methods for you. To have it do so, go to the point in your class at which you'd like to define these methods (often near the bottom), type "equals" and then hit *TAB* twice.

Be sure to customize these methods to use the fields you want these comparisons to be based on. They won't be ready to use as-is!
</aside>

While you may not need to write your own `Equals()` method for each class you create, the more immediate implication for you as a new C# programmer is that you should *always use* `Equals()` yourself when comparing objects. This is especially true when working with objects of types provided by C#, such as `string`. A class that is part of C# or a third-party library will have implemented `Equals()` in a way appropriate for the particular class, whereas `==` will only check to see if two objects are the same literal object.

## Single Responsibility Principle

As we wrap up our whirlwind tour of encapsulation, we want you think a bit about how to go about building good classes. Doing so is more of an art than a science, and it will take you lots of practice and time. However, there are a few rules that we've pointed out to help guide you. Here's one more.

From [Wikipedia][srp]:

<aside class="aside-definition" markdown="1">
The **single responsibility principle** states that every module or class should have responsibility over a single part of the functionality provided by the software, and that responsibility should be entirely encapsulated by the class.
</aside>

It isn't always clear what "responsibility over a single part of the functionality" means. However, it is often very clear what it doesn't mean. For example, we wouldn't think of adding functionality to the `Student` class that tracked all of the data for each of the student's classes, such as catalog number, instructor, and so on. Those are clearly different areas of responsibility. One way to interpret the Single Responsibility Principle is to say that "classes should be small."

As you go forth and create classes, the main thing to keep in mind is that your skill and judgement in creating C# classes will improve over time. The best way to improve is to write lots of code, ask lots of questions, and continue learning!

## References

- [Single Responsibility Principle][srp]
- [Using Constructors (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ms173115.aspx)
- [Object.Equals Method (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/bsc2ak47(v=vs.110).aspx)
- [Object.GetHashCode Method](https://docs.microsoft.com/en-us/dotnet/api/System.Object.GetHashCode?view=netcore-1.0)
- [Object.ToString Method (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/system.object.tostring%28v=vs.110%29.aspx)
- [Reference Types (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/490f96s2.aspx)
- [Value Types (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/s1ax56ch.aspx)

[implementing-equals]: https://msdn.microsoft.com/en-us/library/336aedhh(v=vs.100).aspx
[srp]: https://en.wikipedia.org/wiki/Single_responsibility_principle
