---
title: 'Studio: Area of a Circle'
currentMenu: studios
---

Get cozy with C# syntax by revisiting one of our early Python programs. We'll create a console program that calculates the area of a circle based on input from the user.

## Creating your class

Since you're still new to C# and Visual Studio, we'll provide some extra direction the first few times we go to write code.

Create a new project named `Area` by right-clicking on the top-level "Solution 'csharp-exercises'" item. Select *Add > New Project*. In the modal that opens, make sure "Console Application (.NET Core)" is selected, and enter "Area" in the *Name* field at the bottom of the window. Click *OK*.

You'll write your code in the `Program.cs` file within the Area project.

## Your task

Write a program/class `Area` that prompts the user for a number representing the radius, and then calculates the area of a circle with that radius and prints the result.

> *NOTE:* Recall that the area of a circle is `A = pi * r * r` where `pi` is 3.14 and `r` is the radius.

Here's an example of how your program should work:

```nohighlight
Enter a radius: 2.5
The area of a circle with radius 2.5 is: 19.625
```

Some questions to ask yourself:
- What data type should the radius be?
- What is the best way to get user input into a variable `radius` of that type?

<aside class="aside-warning" markdown="1">
Don't forget to place a `Console.ReadLine()` at the end of your program so the console window remains open after the main portion of your program runs.
</aside>

## Bonus Missions

1. Add validation to your program. If the user enters a negative number, print an error message and quit. You'll need to peek ahead to learn about [conditional syntax in C#](../../csharp4python/control-flow/#conditionals).
2. Extend your program further by using a [while](https://msdn.microsoft.com/en-us/library/2aeyhxcd.aspx) or [do-while](https://msdn.microsoft.com/en-us/library/370s1zax.aspx) loop, so that when the user enters a negative number they are re-prompted.
