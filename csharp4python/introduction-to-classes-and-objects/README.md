---
title: 'Introduction to Classes and Objects'
currentMenu: csharp4python
---

Thus far, we have primarily been examining features of C# that are procedural in nature. Where we have used classes and objects, they have been provided from core C# packages. Over the course of the next few lessons we explore some object-oriented concepts in C#.

In the process, we will introduce the **Three Pillars of Object-Oriented Programming: polymorphism, inheritance, and encapsulation (PIE)**.

## A Minimal Class and Object

We've said several times that classes bundle data and behavior. More formally, classes may contain **fields** (the data) and **methods** (the behaviors). We say that fields and methods are **members** of a class.

Here's the object-oriented version of a "Hello World" class, containing exactly one field and one method.

```csharp
public class HelloWorld {

    string message = "Hello World";

    void SayHello()
    {
        Console.WriteLine(message);
    }

}
```

The only field in this class is the C# `message`, while the only method is `SayHello`, which prints the message and doesn't return anything. Note that there is no `Main` method, so there is no way to run the code in this class directly. We'll need to do that from another class.

To do this, we'll need to create an **instance** of the class `HelloWorld`. Recall from learning about classes and objects in Python that a class is a blueprint for creating objects. We refer to an object created from a particular class as an instance of that class.

Here's how this might look:

```csharp
public class Program {

    public static void Main(string[] args)
    {
        HelloWorld hello = new HelloWorld();
        hello.SayHello();

        Console.ReadLine();
    }
}
```

In order to call the `SayHello` method of `HelloWorld`, we must first have an instance of `HelloWorld`, which we create using the syntax `new HelloWorld()`. As with built-in classes, classes that we create define their own types. So the object `hello` is a variable of type `HelloWorld`.

<aside class="aside-note" markdown="1">
You might be asking, "Didn't we create and call methods before without creating objects?" Indeed we did, but we always used the `static` keyword when doing so. We're taking those chains off now, and will learn how objects and classes work properly, from the ground up.
</aside>

The class `HelloWorld` isn't very interesting, and judged by the standards we will soon learn, it's not particularly good. It only does one thing - print a message - and the message is always the same. Even if we were to create two different objects of type `HelloWorld`, they would be basically be the same.

We introduce this class as a means of illustrating the simplest representation of some basic concepts in C#. The goal of the next few lessons is to build up the machinery to create a wide variety of interesting classes that can be used to create complex programs.

## The this Keyword

In `HelloWorld` above, we could have written `SayHello` this way, with the same net effect:

```csharp
public void SayHello() {
    Console.WriteLine(this.message);
}
```

In this context, inside of the class, we can refer to fields (and methods) that belong to the class using the special object `this`. Whenever you use `this`, it *always* refers to the object that the given code is currently within. Since it is not legal to create code outside of a class, `this` nearly always makes sense to use (there's one exception, that we'll encounter soon).

You are allowed to create local variables -- that is, variables declared within a method -- with the same name as a field of the given class. In this case, in order to refer to the field and not the local variable, we *must* use `this`.

```csharp
public void SayHello() {

    string message = "Goodbye World";

    // prints "Goodbye World"
    Console.WriteLine(message);

    // prints "Hello World"
    Console.WriteLine(this.message);
}
```

<aside class="aside-pro-tip" markdown="1">
When a local variable has the same name as a field, we say that the local variable **shadows** the field. Errors caused by shadowing can be tricky to spot, so it's best to avoid doing this in your code.

If you're following C# naming conventions, fields and local variables both start with a lowercase letter. C# classes also have *properties* which expose field data, and can often be accessed within a class in place of the fields they expose. Properties begin with a capital letter, and therefore do not shadow local method variable names.
</aside>

## Access Modifiers

Every class member has an access level that determines who can access that class. For fields, the access level determines who can directly get or set the value of the field. For methods, the access level determines who can call the method. The access level of a class member is determined by an **access modifier**.

In declaring the `message` field of `HelloWorld`, by omitting an access modifier we implicitly gave it **default access** which for C# means that it will be `private`. It is better to make the access level explicit rather than relying on the default access, so after introducing each of the access modifiers we'll go back and fix this.

We've encountered two access modifiers so far: `public` and `private`. We noted that `public` allows a field or method to be used by anyone, and that `private` allows a field or method to be used only within the class in which it is defined. Two additional access modifiers are available, though they are used much less often than `public` and `private`.

The grid below details these levels, though we haven't really encountered the situations in which they might apply. At this point we introduce them for the sake of completeness. We'll point out specifically where they might be useful when we encounter such scenarios in the future.

Modifier | Class | Assembly | Subclass | World
---------|-------|---------|----------|-------|
`public` | Y | Y | Y | Y
`protected` | Y | N | Y | N
`internal` (default for classes) | Y | Y | N | N
`protected internal` | Y | Y | Y | N
`private` (default for class members) | Y | N | N | N

<aside class="aside-note" markdown="1">
You aren't expected to know the term "subclass" or how it applies to classes yet. We'll learn about it in a future lesson.
</aside>

You can read more about access modifiers at [msdn.microsoft.com][access-modifiers].

Let's fix our class by adding an explicit modifier to `message`.

```csharp
public class HelloWorld {

    private String message = "Hello World";

    public void SayHello() {
        Console.WriteLine(message);
    }

}
```

Since `message` only needs to be used by `SayHello`, we declare it to be `private`.

<aside class="aside-pro-tip" markdown="1">
In C#, you should always use the most restrictive access modifier possible. Minimizing access to class members allows code to be updated more easily in the future, and hides details of how you implement your classes from others.

This makes your code more modular and modifiable. Each public member that you expose is another field or method that can be referenced directly elsewhere in any program using your class. Thus, changing any such field or method in your code could potentially break any code referencing such members. The fewer public members, the more you can change your code without breaking stuff elsewhere.
</aside>

- [Access Modifiers in C# (msdn.microsoft.com)][access-modifiers]
- [Using the this Keyword (docs.oracle.com)](https://docs.oracle.com/csharpse/tutorial/csharp/csharpOO/thiskey.html)


[access-modifiers]: https://msdn.microsoft.com/en-us/library/ms173121.aspx
