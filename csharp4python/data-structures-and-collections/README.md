---
title: Data Structures and Collections
currentMenu: csharp4python
---

C# provides powerful and flexible ways to store data. We'll introduce only a few here, but they will be sufficient for all of your basic needs while you get going with C#.

## Ordered Data: Lists and Arrays



### List

To write the C# version of this program we will have to introduce several new C# concepts. We will see the C# equivalent of a list, called a `List.` We will also introduce different kinds of loops used in C#.

Here is the C# code needed to write the exact same program:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace Gradebook
{
    public class Program
    {
        public static void Main(string[] args)
        {
            List<string> students = new List<string>();
            List<double> grades = new List<double>();
            string newStudent;

            Console.WriteLine("Enter your students:");

            // Collect student grades until user enters blank line
            do
            {
                newStudent = Console.ReadLine();
                if (newStudent != "")
                {
                    students.Add(newStudent);
                }
            }
            while (newStudent != "");

            // Get student grades
            foreach (string student in students)
            {
                Console.Write("Grade for " + student + ": ");
                double aGrade = double.Parse(Console.ReadLine());
                grades.Add(aGrade);
            }

            // Print roster
            Console.WriteLine("Student roster:");
            for (int i = 0; i < students.Count; i++)
            {
                Console.WriteLine(students[i] + " (" + grades[i] + ")");
            }

            double sum = grades.Sum();
            double avg = sum / grades.Count;
            Console.WriteLine("Average grade: " + avg);

            Console.ReadLine();
        }
    }
}
```

Before going any further, I suggest you try to compile the above program and run it.

Once you've done that, let's look at what is happening in the C# source. The

```csharp
List<string> students = new List<string>();
List<double> grades = new List<double>();
string newStudent;
```

Here we declare an initialize two objects, `students` and `grades`, which appears to be of type `List<string>` and `List<double>`, respectively. A `List` in C# is very similar to a list in Python, with one imporant difference. Unlike Python, where lists can contain any type of value, in C# we must let the compiler know what kind of objects our list is going to contain. In the case of `students`, the `List` will contain values of type `string` (representint the names of the students), so we use the `List<string>` syntax to inform the compiler that we intend to fill our list with strings. Similarly, `grades` will hold exclusively values of type `double` and is declared to be of type `List<double>`.

We also initialize each list by creating a new, empty list. Note that when we call the `List` constructor, as in `new List<string>()`, we must specify the same type as we do in the declaration.

<aside class="aside-note" markdown="1">
You will sometimes see the `List` class written as `List<T>`, where `T` represents a placeholder for the type that a programmer will declare a given list to hold. This is especially true in documentation. You cna think of `T` as reprsenting an arbitrary type.

Classes like `List<T>` that take another type or class as a parameter are referred to as **generic classes** or **generic types**.
</aside>

TODO - do-while loop; lists are flexible in size

TODO - for loop; indexing into lists

TODO - foreach loop

TODO - Sum method and extensions; additional methods

The syntax of this for loop probably looks very strange to you, but in fact it is not too different from what happens in Python using `range`. They syntax `for(Integer i = 0; i < 10; i++)` is exactly equivalent to the Python `for i in range(10)`. The first statement inside the parenthesis declares and initializes a loop variable `i`. The second statement is a Boolean expression that is our exit condition. In other words, we will keep looping as long as this expression evaluates to true. The third statement is used to increment the value of the loop variable at the end of iteration through the loop. The syntax `i++` is C# shorthand for `i + 1`. C# also supports the shorthand `i--` to decrement the value of `i`. Like Python, you can also write `i += 2` as shorthand for `i = i + 2`.

Consider the next segment:

```csharp
for (int j = 0; j < data.Length; j++) {
    int val = int.Parse(data[j]);
    count[val] = count[val] + 1;
}
```

We are iterating through the `data` array in order to update the number of occurences of each value.

The line `count[val] = count[val] + 1;` illustrates another important difference between Python and C#. Notice that while `count` is of type `List` we can still use the square bracket operator `[]` to retrieve a value from the list, just as we can with Python lists.

Let's consider the last loop in this program:

```csharp
int idx = 0;
foreach (int k in count) {
    Console.WriteLine(idx + " occurred " + k + " times");
    idx++;
}
```

This is similar to the Python for loop where the object of the loop is a sequence. In C# we can use this kind of for loop over all kinds of sequences, which are called Collection classes in C#. The loop `for(Integer i : count)` is equivalent to the Python loop `for i in count:`. This loop iterates through each of the elements in the `List` named `count`. Each time through the loop, the `Integer` variable `i` is assigned the value of the next element of the `List`. If you tried the experiment of removing the `<int>` part of the `List` declaration you probably noticed that you had an error on this line. Why?

### Arrays

As we noted at that beginning of this section, we are going to use the C# `List` type to store simple sets of data. They are easy to use and more closely match the way that Python lists behave.

However, you should be aware that C# also has a more primitive data structure called an array. In fact, you have already seen one example of an array declared in the Hello World program (`string[] args`).

Why does C# have both arrays and `List`? The answer is likely historical, in part at least. C# is a C-style language, and arrays are the most basic data structure in C. Additionally, using an array over a `List` might be preferred in some circumstances, primarily for performance reasons (arrays operations are generally faster). Also note that arrays are of fixed size. You can not expand or contract an array after it is created, so you must no exactly how many elements it will need to hold.

To illustrate array usage, here is a version of the `Histo` program/class that uses primitive arrays instead of a `List`:

```csharp

```

The main difference between this example and the previous example is that we declare count to be an array of integers: `int[] count = {0,0,0,0,0,0,0,0,0,0};`. This syntax initializes an array directly. Notice that we use the square bracket notation to index into an array: `count[idx]`.

## Key/Value Data: Dictionaries

Just as Python provides the dictionary structure to allow us to store data as key/value pairs, C# also provides us a similar mechanism. Rather than the dictionary terminology, C# calls these objects Maps. There are multiple types of maps, but we'll focus only on the most general purpose map type: `HashMap`.

Let's stick with a simple frequency counting example, only this time we will count the frequency of words in a document. A simple Python program for this job could look like this:

```python
def main():
    data = open('alice.txt')
    wordList = data.read().split()
    count = {}
    for w in wordList:
        w = w.lower()
        count[w] = count.get(w,0) + 1

    keyList = sorted(count.keys())
    for k in keyList:
        print("%-20s occurred %4d times" % (k, count[k]))

if __name__ == '__main__':
    main()
```

The file `alice.txt` contains a short snippet from the beginning of *Alice In Wonderland*. You may [view the file's contents](TODO).

Notice that the structure of the program is very similar to the numeric histogram program.

Here's the C# version, using instances of the `Dictionary` class:

```csharp

```

As an exercise, see if you can improve the program above to ignore punctuation.

## References

- [List (msdn.microsoft.com)]()
- [Dictionary (msdn.microsoft.com)]()
- [Array (msdn.microsoft.com)]()
