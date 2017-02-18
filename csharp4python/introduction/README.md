---
title: Introduction
currentMenu: csharp4python
---

We will use Python as a starting point for our journey into [C#](https://en.wikipedia.org/wiki/C#_(programming_language)). We will begin by looking at a very simple C# program, just to see what the language looks like and how we get a program to run. Next, we will look at the main constructs that are common to most programming languages. These concepts are part of what is generally referred to as [procedural programming](https://en.wikipedia.org/wiki/Procedural_programming).

- Data Types
- Console Input and Output
- Loops
- Conditionals

Once we have the basics of C# behind us we will move on to look at the features of C# that are both unique and powerful. These features bring us into the areas of [object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming) and [data structures](https://en.wikipedia.org/wiki/Data_structure).

- Classes
- Interfaces
- Collections

## Why Learn Another Programming Language?

Python is great first programming language for several reasons. The syntax is sparse and clear. The underlying model of how objects and variables work is very consistent. You can write powerful and interesting programs without a lot of work. However, Python is representative of one kind of language, called a dynamic language. You might think of Python as being fairly informal. There are other languages, like C# and C++ that are more formal.

These languages have some advantages of their own. For very large, languages like programs C# and C++ are going to give you the best performance. They are also much more "safe" and "maintainable". A lot of what makes Python easy to use is that you must remember certain things. For example, if you set a variable `x` to reference a turtle, and forget later that `x` is a turtle but try to invoke a string method on it, you will get an error upon running your program. C# and C++ protect you by forcing you to be upfront and formal about the kind of object each variable is going to refer to. This means that some types of errors are caught sooner, and the runtime behavior of a program is more dependable.

In one sense, Python is representative of a whole class of languages, sometimes referred to as "scripting languages." Other languages in the same category as Python are Ruby and Javascript. C# is representative of what I will call industrial strength languages. These languages are good for projects with several people working on the project where being formal and careful about what you do may impact lots of other people. Languages in this category include C++, C, and Java.

Programming languages will always change. As the field of computer science advances there will be new programming languages, and you will need to learn some of them. As you do, you will see that there are certain features that most programming languages have in common -- variables, loops, conditionals, functions -- and there are some features that are unique to each. If you know what is common in languages, that is a good place to start.

## Why Learn C#?

C# has been widely used by programmers for over 20 years. It continues to grow and to evolve, and to be extremely relevant to both programmers and companies using and building software. At a high level, this can easily be seen by looking at measures of language popularity and usage, such as the [Tiobe Index](http://www.tiobe.com/tiobe-index/) or [GitHut](http://githut.info/). In addition, C# is a [C-style language](https://en.wikipedia.org/wiki/Category:C_programming_language_family), meaning that many of its sytnax features are derivative of the [C programming language](https://en.wikipedia.org/wiki/C_(programming_language)). This makes learning the basics of other C-style languages relatively straightforward once you know C# (or vice versa).

C# is an enormous language. We could not begin to scratch the surface of the langauge even if we devoted all of our time to the task. However, C# is very powerful and we will write some very powerful programs in this course.

## Getting Ready

Before starting with each of these lessons, open up Visual Studio and make sure you have the `csharp-exercises` solution open. All C# examples in these lessons are provided in this folder, and you should run the programs there as you go, modifying and experimenting with the code to help you learn.

> *NOTE:* When looking at source code for these examples in Visual Studio, you will notice that they vary slightly from code included here. In these lessons, we omit `using` statements, top-level comments, and other inconsequential elements.

> *NOTE:* We'll use Python 3 in each of our Python examples.

## Hello, World

As with learning Python, we'll start by writing a "Hello, World" program. There are no logic errors to make, so getting it to run relies only on understanding the most basic syntax rules of the language.

### Comments

Before looking at our "Hello World" program, let's start by covering the easiest piece of syntax in any programming language: comments.

In Python we were able to insert comments in two ways. Single line comments begin with `#` and multi-line comments (aka docstrings) are surrounded by triple-quotes, `"""`.

```python
# This comment lives on a single line

"""this comment
can span
multiple lines
"""
```

We have similar functionality in C#, but with `//` denoting single-line comments and `/*` and `*/` surrounding multi-line comments.

```csharp
// This comment lives on a single line

/*
this comment
can span
multiple lines
*/
```

Throught these initial lessons, we'll use a short comment at the top of each code sample to indicate which language is being used, to help you quickly tell while you're making the transition to C#. Here's an example:

```csharp
...some C# code...
```
### Hello, World in Python

Let's first look a version of Hello, World for Python:

```python
print("Hello, World")
```

If you put this code in a file named `helloworld.py`, you could run it within a terminal by issuing the command `python3 helloworld.py`. Of course, it would then print `Hello, World` to the terminal.

Let's take this example one step further, to draw a closer parallel to what we'll see in C#. Consider the following, more complicated program.

```python
def main():
    print("Hello, World")

if __name__ == '__main__':
    main()
```

Here, we've added a "wrapper" to our simple call to the `print` function, in the form of a `Main` function. Recall that the last two lines of the program check to ensure that the file is being run directly, rather than being imported as a module into another Python file. Running the program with `python3 helloworld.py` results in the same output as the first example.

### Hello, World in C&#35;

Here is the a C# program with the same functionality as the Python Hello, World program:

```csharp
namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
            Console.ReadLine();
        }
    }
}
```

Comparing this to the Python version above, the only real similarities we see are the "Hello World" string and functions that seem to indicate they print a message (`print` and `Console.WriteLine`). However, there is more that's different than the same. Do not worry! An important skill for a programmer is to learn what to ignore and what to look at carefully. You will soon find that there are some elements of C# that will fade into the background as you become used to seeing them.

This simple example illustrates a few very important C# rules:

1. Every C# program must define a class; all code is inside a class
2. Everything in C# must have a type
3. Every C# program (though not every class) must have a function (or method) called `Main` that has a signature\* of `static void Main(string[] args)`

\* A **method signature** specifies all of the information necessary for a programmer to use the method, including, at minimum, it's name and the number, types, and order of its parameters. It can also include access and static modifiers (we'll learn about these later).

Let's take this example one bit at a time to see how these rules are applied.

#### Namespace and Class Declarations

Our program starts with `namespace HelloWorld`. Namespaces organize our code into different "packages". We'll learn more about these as we go, but for now just know that each project that we create in Visual Studio will have it's own namespace. Furthermore, a **code block** is defined with curly braces (`{` and `}`) to specify which code is part of the namespace.

We then encounter `class Program`. The `class` keyword indicates that we are defining a class, while `Program` is the name of the class. The name of a class is up to the programmer, and can be anything that fits within some basic rules (names must start with a letter, may not contain spaces, and so on). When naming classes it's best to follow [C# naming conventions][naming-conventions].

You will notice that we indented this line once, as it sits one level inside of our class definition. Unlike in Python, such indentation is not required; it is simply a convention applied for the purpose of readability and consistency. Instead of indentation, what signifies to the compiler that this class definition is part of the `HelloWorld` namespace is the fact that it is part of the block associated with that namespace. In other words, it's the outer set of curly braces that make this explicit.

Unlike Python, where a program can simply be a bunch of statements in a file, C# programs must be inside a class. The `Program` class is not a very useful class since it has no instance variables and only one method. It is created out of necessity.

When defining a class, we must surround the contents of the class (it's properties and methods) with "curly braces": `{` and `}`. These braces will also be used to surround conditionals, methods, and loops in coming lessons. In C#, any section of code encolsed in a pair of such braces is referred to as a **block**.

#### Main method

On the next line we start our method definition. The name of this method is:

```csharp
static void Main(string[] args)
```

Everything on this line is significant, and is part of the identification of this method. For example, the following lines look similar but are in fact treated by C# as completely different methods:

- `static void Main(string[] args)`
- `static void Main()`
- `void Main(String args)`

Disecting this one line could easily take us very deep into the world of C#, but we'll be cautious to not get pulled to far in too soon. Each of these concepts can and will be explored in much more depth later.

##### static

The next word, `static`, tells C# that this is a method that is part of the class, but does not belong to any one instance of the class. Rather, it is shared by all instances. Recall that a class is a blueprint for a type of object, and when we create an object based on a class, we refer to that object as an **instance** of the class (or just **instance**).

The kind of methods we typically wrote in Python required an instance in order for the method to be called. With a static method, the object to the left of the `.` is a class, not an instance of the class. The way that we would call the `Main` method directly is: `Hello.main(parameter1)`. For now you can think of static methods the same way you think of methods in Python modules that don’t require an instance. For example, the math module contains many methods: `sin`, `cos`, etc. You evaluated these methods using the names `math.cos(90)` or `math.sin(60)`.

##### void

The next word, `void`, tells the C# compiler that the method `Main` will not return a value. This is roughly analogous to omitting the return statement in a Python method. The method will run to completion and exit but will not return a value that you might use in an assignment statement. As we look at other examples we will see that every C# function must tell the compiler what kind of an object it will return. This is in keeping with the rule that says everything in C# must have a type. In this case we use the special type called `void` which means nothing will be returned.

##### Main

Next we have the proper name for the method: `Main`. The rules for names in C# are similar to the rules in Python. Names can include letters, numbers, and the `_`. Names in C# must start with a letter.

##### string[] args

Finally, we have the parameter list for the method. In this example we have one parameter, named `args`. Everything in C# must have a type, so we also have to tell the compiler that the value of `args` is an array of strings. For the moment you can just think of an array as being the same thing as a list in Python. The practical benefit of declaring that the method `Main` must accept one parameter and the parameter must be a an array of strings is that if you call `Main` somewhere else in your code and pass it an array of integers or even a single string, the compiler will flag it as an error. In Python we would not have seen such an error manifest itself until we ran the program.

#### Console.WriteLine

That is a lot of new material to digest in only a single line of C#. Let's look at the next line: `Console.WriteLine("Hello World!");`. This line should look a bit more familiar to you. Python and C# both use the dot notation for finding names.

In this example we start with `Console`. `Console` is a class. Within the `Console` class, C# will now call the method named `WriteLine(string s)` on that object. The `WriteLine` method prints a string and adds a newline character at the end. Anywhere in Python that you used the `print` function you will use the `Console.WriteLine` method in C#.

#### Console.ReadLine

Similar to `WriteLine`, the `ReadLine` method of the `Console` class will read input from the user's console. In this case, we don't need to do anything with the user's input, we simply want the program to wait until the user hits Enter before exiting.

##### Semi-colon

There is one more character on these two lines that are significant, and that is the `;` at the end. In C#, the `;` signifies the end of a statement. Unlike Python where statements are almost always only one line long, C# statements can spread across many lines. The compiler knows it has reached the end of a statement when it encounters a `;`. This is a very important difference to remember. In C# the following statements are all legal and equivalent. We do not encourage you to write your code in any way other than the first example, but you should know that it is legal.

```csharp
Console.WriteLine("Hello World!");
```

```csharp
Console.WriteLine("Hello World!")
;
```

```csharp
Console.WriteLine
    (
     "Hello World!"
    )     ;
```

```csharp
Console
   .WriteLine("Hello World!")
    ;
```

> *NOTE:* In contrast to Python, indentation (and whitespace, in general) *does not* hold any special meaning in C#.

####

If we wanted to translate the C# back to Python, we would have something like the following class definition:

```python
class Hello(object):

    @staticmethod
    def main(args):
        print "Hello World!"
```

Notice that we used the decorator `@staticmethod` to tell the Python interpreter that `main` is going to be a static method. The impact of this is that we don’t have to, indeed we should not, use `self` as the first parameter of the `main` method! Using this definition we can call the `main` method in a Python session like this:

```nohighlight
>>> Hello.main("")
Hello World!
>>>
```

## References

- [C Sharp (programming language) (wikipedia.org)](https://en.wikipedia.org/wiki/C_Sharp_(programming_language))
- [Namespaces (msdn.microsoft.com)]](https://msdn.microsoft.com/en-us/library/0d941h9d.aspx)

[naming-conventions]: ../naming-conventions/
