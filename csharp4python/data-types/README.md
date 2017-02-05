---
title: Data Types
currentMenu: csharp4python
---

How C# handles values and variables is one of the most significant differences it and Python.

## Static vs. Dynamic Typing

Python is a **dynamically typed** language. In a dynamically typed language a variable or parameter can refer to any kind of value at any time. When the variable is used, the interpreter figures out what type it is and behaves accordingly.

C# is a **statically typed** language. In a statically typed language the association between a variable or parameter and the type of value it can refer to is determined *when the variable or parameter is declared*. Once the declaration is made it is an illegal for a it to refer to a value of any other type.

For example, this is legal in Python:

```python
# Python
x = "dog"
x = 42
```

If we were to inspect the type of `x` after the first line executes (e.g. using Python's `type()` function) we would find that it was a string. After the next line executes, it is an integer. `x` is allowed to hold values of different types.

However, the corresponding code in C# will result in a build error:

```csharp
// C#
string x = "dog";
x = 42;
```

The compiler error would occur when we try to assign `42` to a variable of type `string`. This is simply not allowed in C#.

Formally, this means that *we must declare the type of every variable and parameter* in a statically typed language. This is done by preceding the variable or parameter name with the name of its type, as we did in the example above: `string x = "dog"`.

We only need to specify the type of a variable or paremeter when declaring it. Subsequent usage does not require specifying the type, and will result in an error.

It is allowed in some situations in C# to declare a variable without specifying a type by using the keyword `var`, as in `var x = "dog";`. In this case, C# still assigns a type to `x` through inference. It looks and sees that we are assigning `x` the value `"dog"`, which is `string`. Thus, `x` has type `string` and attempting to assign `x = 42` will still result in a build error. We recommend avoiding use of `var` while you are learning C#, and even after you become more experienced with the langauge you will still only want to use it sparingly and in specific circumstances. Explicitely declaring the type of your variables makes for more readable code, in general.

Dynamic and static typing are examples of different [type systems](https://en.wikipedia.org/wiki/Type_system). The type system of a programming language is one of the most important high-level characteristics that programmers use when discussing the differences between languages. Here are a few examples of popular languages falling into these two categories:
    - **Dynamic**: Python, Ruby, C#script, PHP
    - **Static**: C#, C, C++, Java, Ada

This major difference between Python and C# will mean that we'll need to pay much more attention to types when writing C#. Let's begin by exploring the most common and important data types in this language.

## string

Strings in C# and Python are quite similar. Like Python, C# strings are immutable. However, manipulating strings in C# is not quite as obvious since strings do not support an indexing or slicing operator. That is not to say that you can’t index into a C# string; you can. You can also pull out a substring just as you can with slicing. The difference is that C# uses method calls where Python uses operators.

The table below maps common Python string operations to their C# counterparts. For the examples shown in the table, we will use a string variable called `str`.

Python | C# | Description
|------|------|-------------|
`str[3]` | `str.Substring(3,1)` | Return character in 3rd position
`str[2:5]` | `str.Substring(2,3)` | Return substring from 2nd to 4th, i.e. substring starting at index 2 and 3 characters long
`len(str)` | `str.Length` | Return the length of the string
`str.find('x')` | `str.IndexOf('x')` | Find the first occurrence of `'x'`
`str.split(',')` | `str.split(',')` | Split the string at `','` into a list/array of strings
`str + str` |  `str + str` | Concatenate two strings together
`str.strip()` | `str.Trim()` | Remove any whitespace at the beginning or end
`str.lower()` | `str.ToLower()` | Return a copy of `str` with all characters lowercase

## Numeric

One of the great things about Python is that all of the basic data types are objects. In C# this is also the case, though the so-called built-in data types also have short names that differ from typical class name conventions.

We provide here a list of some of the most common types, along with both short and class names. We'll generally prefer to use the short names for each of these.

Short name | .NET Class | Examples | Notes
|---------|--------|----------|-------|
`int` | `Int32` | -5 <br> 1024 | &nbsp;
`float` | `Single` | 1.212 <br> 3.14 | &nbsp;
`double` | `Double` | 3.14159 <br> 2.0 | Doubles are twice as precise (i.e. can hold much longer decimal numbers) than floats
`char` | `Char` | 'a' <br> '!' | A single Unicode character. Must be enclosed in single quotes `''` to be a character; double quotes `""` indicate a string
`string` | `String` | "LaunchCode" <br> "a" | A sequent of characters. Must be encolosed in double quotes `"`; single quotes `'` indicate a character
`bool` | `Boolean` | `true` <br> `false` | Note that booleans in Java are not capitalized as they are in Python.

Not all built-in data types in C# are listed here, only the most commonly used types that beginners are likely to encounter. If you're curious, [read more about built-in types in C#](https://msdn.microsoft.com/en-us/library/ya5y69ds.aspx)

## Example: The TempConv Program

Lets go back in time and look at another of our very early Python programs. Here is a simple Python function to convert a Fahrenheit temperature to Celsius.

```python
# Python
def main():
    fahrenheit = int(input("Enter the temperature in F: "))
    celsuis = (fahrenheit - 32) * (5.0 / 9.0)
    print("the temperature in C is: ", celsuis)

if __name__ == '__main__':
    main()
```

Next, lets look at the C# Equivalent.

```csharp
// C#
using System;

namespace TempConv
{
    class Program
    {
        static void Main(string[] args)
        {
            double fahrenheit;
            double celcius;
            string input;

            Console.WriteLine("Tempperature in F:");
            input = Console.ReadLine();
            fahrenheit = double.Parse(input);

            celcius = (fahrenheit - 32) * 5 / 9;
            Console.WriteLine("The Temperature in C is: " + celcius);
            Console.ReadLine();
        }
    }
}
```

There are several new concepts introduced in this example. We will look at them in the following order:

- `using` statement
- Variable declaration
- Input/output and the `Console` class

### using

In C#, you can use any class that is available without having to import the class subject to two very important conditions:

1. The C# compiler must know that the class exists
2. You must use the full name of the class

How does the compiler know that certain classes exist? We have these rules:

(TODO - explain "classpath" rules)

You can think of the `using` statement in C# as working a little bit like the `from module import xxx` statement in Python. However, behind the scenes the two statements actually do very different things.

The first important difference to understand is that the class naming system in C# is very hierarchical. The *full* name of the `Console` class is really `System.Console`. You can think of this name as having two parts: The first part, `System`, is called the **namespace**, and the last part is the class. We’ll talk more about the class naming system a bit later. The second important difference is that it is not the `using` statement’s responsibility to load classes into memory. That task falls on the **assembly**, which is the unit of compiled code created by Visual Studio (or the C# compiler, more generally).

The `using` statement tells the compiler that we are going to use a shortened version of the class’s name. In this example we are going to use the class `System.Console`, but we can refer to it as just `Console`. We could use the `System.Console` class without any problem and without any import statement provided that we always referred to it by its full name.

Don't just trust us, try it yourself! Remove the `using` statement and change `Console` to `System.Console` in the rest of the code. The program should still compile and run.

### Declaring Variables

In the example above, these lines contain variable declarations:

```csharp
// C#
double fahrenheit;
double celsius;
string input;
```
Specifically we are saying that `fahrenheit` and `celsius` are going to reference objects that are of type `double`. The variable `input` will contain a string. This means that if we were to try an assignment like `fahrenheit = "xyz"` the compiler would generate an error because `"xyz"` is a string and `fahrenheit` is supposed to be a double.

For Python programmers the following error is likely to be even more common. Suppose we forgot the declaration for `celsius` and instead left that line blank. What would happen if we try to run our program?

![Build error](build-error.png)

The compiler detects an error and Visual Studio displays this message. Where you to look at the error pane, you would see the message: "The name 'celcius' does not exist in the current context".

> *NOTE:* When using an IDE such as Visual Studio, your code is typically checked by the IDE's built-in compiler as you write your code. Thus, errors are usually visually indicated within your code by the IDE as you write your code, saving you the extra step of having to explicitely compiling your code before finding compiler errors. Nice, huh?

The general rule in C# is that you must decide what kind of an object your variable is going to reference and then you must declare that variable before you use it. There is much more to say about the static typing of C# but for now this is enough.

### Input / Output and the Console Class

Console input and output is facilitated by the class `System.Console`. We'll rely heavily on just two methods of this class: `Console.WriteLine` and `Console.ReadLine`.

`Console.WriteLine` can take parameters of various types, including `string`, `char`, `double`, `bool`, and others. However, unlike the `print` function in Python, we can only provide it with a single argument. Thus, we'll need to manually concatenate strings and other values, converting types if necessary. As with Python, a newline character is output after the given message.

```python
# Python
year = 2017
print("Hello", "World")
print("The year is:", year)
```

```csharp
// C#
int year = 2017;
Console.WriteLine("Hello" + "World")
Console.WriteLine("The year is " + year.ToString());
```

Similarly, `Console.ReadLine` returns input as a string. To convert it to a desired type, you can generally use the syntax `*type*.Parse(value)`, as in this example:

```csharp
// C#
string input = Console.ReadLine();
int year = int.Parse(input);
```

This is very similar to what we did in Python:

```python
# Python
user_input = input()
year = int(user_input)
```

## References

- [String Methods (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/system.string_methods(v=vs.110).aspx)
- [The `Console` class (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/system.console(v=vs.110).aspx)
