---
title: Control Flow
currentMenu: csharp4python
---

In this section we examine the syntax of control flow statements n C# -- conditionals and loops -- comparing them to Python. We will find them to be very similar, with relatively predictable syntax variations based on the C# that we have learned to this point.

## Conditionals

Conditional statements in Python and C# are very similar. In Python we have three patterns.

### Simple if

Let's consider an `if` statement with no `else` clause. Here's the Python version.

```python
if condition:
    statement1
    statement2
    ...
```

In C# this same pattern is simply written as:

```csharp
if (condition)
{
    statement1
    statement2
    ...
}
```

Once again, you can see that in C# the curly braces define a block rather than indentation. In C#, the parentheses around the condition are required.

### if-else

Adding an `else` clause, we have:

```python
if condition:
    statement1
    statement2
    ...
else:
    statement1
    statement2
    ...
```

In C# this is written as:

```csharp
if (condition)
{
    statement1
    statement2
    ...
}
else
{
    statement1
    statement2
    ...
}
```

### elif / else if

In C# we can utlize the same behavior that `elif` provides in Python, with a slightly different syntax. Here is a simple example in both Python and C#.

```python
grade = int(input('enter a grade'))
if grade < 60:
    print 'F'
elif grade < 70:
    print 'D'
elif grade < 80:
    print 'C'
elif grade < 90:
    print 'B'
else:
    print 'A'
```

In C# we would write this as follows:

```csharp
public class ElseIf {
    public static void main(string args[]) {
        int grade = 85;
        if (grade < 60)
        {
            Console.WriteLine('F');
        }
        else if (grade < 70)
        {
            Console.WriteLine('D');
        }
        else if (grade < 80)
        {
            Console.WriteLine('C');
        }
        else if (grade < 90)
        {
            Console.WriteLine('B');
        }
        else
        {
            Console.WriteLine('A');
        }
    }
}
```

### switch

C# also supports a `switch` statement that acts something like the `elif` statement of Python under certain conditions.

The `switch` statement is not used very often, and we generally recommend you avoid using it. It is not as powerful as the `else if` model because the switch variable can only be compared for equality with a very small class of types.

Here's a quick example:

```csharp
class Program
{
   static void Main(string[] args)
   {
       Console.WriteLine("Enter an integer: ");
       string input = Console.ReadLine();
       int dayNum = int.Parse(input);

       string day;
       switch (dayNum) {
           case 0:
               day = "Sunday";
               break;
           case 1:
               day = "Monday";
               break;
           case 2:
               day = "Tuesday";
               break;
           case 3:
               day = "Wednesday";
               break;
           case 4:
               day = "Thursday";
               break;
           case 5:
               day = "Friday";
               break;
           case 6:
               day = "Saturday";
               break;
           default:
               day = "Int does not correspond to a day of the week";
               break;
       }

       Console.WriteLine(day);
       Console.ReadLine();
   }
}
```

## Iteration

At a conceptual level, loops in C# aren't that different from loops in Python, though the syntax varies significantly in some cases.

### For Loops

In Python the easiest way to write a definite loop (aka a for loop) is using the for loop in conjunction with the range function. For example:

```python
for i in range(10):
   print i
```

In C# we would write this as:

```csharp
for (int i = 0; i < 10; i++ )
{
    Console.WriteLine(i);
}
```

Recall that the `range` function provides you with a wide variety of options for controlling the value of the loop variable.

```python
range(stop)
range(start,stop)
range(start,stop,step)
```

The C# for loop is really analogous to the last option giving you explicit control over the starting, stopping, and stepping in the three clauses inside the parenthesis. You can think of it this way:

```csharp
for (start clause; stop clause; step clause)
{
    statement1
    statement2
    ...
}
```

If you want to start at 100, stop at 0 and count backward by 5 the Python loop would be written as:

```python
for i in range(100,-1,-5):
    print i
```

In C# we would write this as:

```csharp
for (int i = 100; i >= 0; i -= 5)
{
    Console.WriteLine(i);
}
```

In Python the for loop can also iterate over any sequence such as a list, a string, or a tuple. C# also provides a variation of its for loop that provides the same functionality in its so called *for-each* loop.

In Python we can iterate over a list as follows:

```python
l = [1, 1, 2, 3, 5, 8, 13, 21]
for fib in l:
   print fib
```

In C#, this would look like:

```csharp
int l[] = {1, 1, 2, 3, 5, 8, 13, 21};
foreach (int i in l) {
    Console.WriteLine(i);
}
```

This version translates nicely to iterating through a string, where the string acts essentially like an array of characters:

```csharp
string msg = "Hello World";
foreach (char c in msg) {
    Console.WriteLine(c);
}
```

### While Loops

Both Python and C# support the while loop, or indefinite loop. Recall that in Python the while loop is written as:

```python
while condition:
   statement1
   statement2
   ...
```

In C# we add parenthesis and curly braces to get:

```csharp
while (condition)
{
    statement1
    statement2
    ...
}
```

C# adds an additional, if seldom used, variation of the while loop called the do-while loop. The do-while loop is very similar to while except that the condition is evaluated at the end of the loop rather than the beginning. This ensures that a loop will be executed at least one time. Some programmers prefer this loop in some situations because it avoids an additional assignment prior to the loop. For example:

```csharp
do
{
    statement1
    statement2
    ...
} while (condition);
```

## References

- [for statment (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ch45axte.aspx)
- [foreach statement (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ttw7t8t6.aspx)
- [switch (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/06tc147t.aspx)
