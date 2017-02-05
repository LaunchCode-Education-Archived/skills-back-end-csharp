---
title: Data Structures and Collections
currentMenu: csharp4python
---

C# provides powerful and flexible ways to store data. We'll introduce only a few here, but they will be sufficient for all of your basic needs while you get going with C#.

## Ordered Data: Lists and Arrays

Lets look at another early Python program. We are going to read numbers from a file and produce a histogram that shows the frequency of the various numbers. The data file we will use has one number between 0 and 9 on each line of the file. Here is a simple Python program that creates and prints a histogram.

```python
# Python
def main():
    count = [0]*10
    data = open('test.dat')

    for line in data:
        count[int(line)] = count[int(line)] + 1

    idx = 0
    for num in count:
        print idx, " occured ", num, " times."
        idx += 1

if __name__ == '__main__':
    main()
```

Let's use a data file that contains the following text:

```nohighlight
9 8 4 5 3 5 2 1 5
```

> *NOTE:* When running the example code, note that `test.dat` is located at the root of the project, since this is where the `File` class will look for it by default. To use a file in another directory, we would need to provide a specific path to the file.

We will get output that looks like this:

```nohighlight
0 occurred 0 times
1 occurred 1 times
2 occurred 1 times
3 occurred 1 times
4 occurred 1 times
5 occurred 3 times
6 occurred 0 times
7 occurred 0 times
8 occurred 1 times
9 occurred 1 times
```

Let's review what is happening in this little program. In the first line we create a list and initialize the first 10 positions in the list to be 0. Next we open the data file called `test.dat`. We then have a loop that reads each line of the file. As we read each line, we convert it to an integer and increment the counter at the position in the list indicated by the number on the line we just read. Finally, we iterate over each element in the list printing out both the position in the list and the total value stored in that position.

### List

To write the C# version of this program we will have to introduce several new C# concepts. We will see the C# equivalent of a list, called an `ArrayList.` We will also introduce three different kinds of loops used in C#.

Here is the C# code needed to write the exact same program:

```csharp
// C#
namespace Histo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Pull in data from a file as configured as a project resource
            string rawData = Histo.Properties.Resources.test_data;
            string[] data = rawData.Split(' ');

            // Fill the list with zeros
            List<int> count = new List<int>();
            for (int i = 0; i < data.Length; i++) {
                count.Add(0);
            }

            // Count occurences of each number in the file
            for (int j = 0; j < data.Length; j++) {
                int val = int.Parse(data[j]);
                count[val] = count[val] + 1;
            }

            // Display results
            int idx = 0;
            foreach (int k in count) {
                Console.WriteLine(idx + " occurred " + k + " times");
                idx++;
            }

            Console.ReadLine();
        }
    }
}
```

Before going any further, I suggest you try to compile the above program and run it. Try altering the test data in `Histo/Resources/test_data.txt`.

Let's look at what is happening in the C# source. Here are the first two lines.

```csharp
// C#
string rawData = Histo.Properties.Resources.test_data;
string[] data = rawData.Split(' ');
```

They pull in data from a file that is configured as a **project resources**. We won't go into how this file input mechanism works since we'll only use it in a couple of instances. The important thing for you to know is that the contents of the file are pulled into a string. In this case, our data has the form of a collection of integers separated by single spaces, so we can use `string.Split` to separate it into individual strings, one for each "number" (the data is still stored as an array of strings).

Moving on to the next segment, we consider these lines:

```csharp
// C#
List<int> count = new List<int>();
for (int i = 0; i < data.Length; i++) {
    count.Add(0);
}
```

Here we declare an initialize `count`, which appears to be of type `List<int>`. A `List` in C# is very similar to a list in Python, with one imporant difference. Unlike Python, where lists can contain just about anything, in C# we must let the compiler know what kind of objects our list is going to contain. In this case, the `List` will contain integers, so we use the `List<int>` syntax to inform the compiler that we intend to fill our list with integers.

TODO - finish explaining code above

The following lines are required to pull in data from the file.

```csharp
// C#
string rawData = Histo.Properties.Resources.test_data;
```

TODO - explain this and other file i/o approach

Let's consider the next segment of our program:

```csharp
// C#
List<int> count = new List<int>();

for (int i = 0; i < data.Length; i++) {
    count.Add(0);
}
```

We create a `List` that will hold integers by calling the `List` constructor. The list will grow or shrink dynamically as needed, just like a list in Python. It's possible to give the `List` constructor a size, but omitting a size allows for more flexibility. We then start the first of three loops. The first is **for loop** that serves the same purpose as the Python statement `count = [0]*10`. That is, it initializes the first 10 positions in the `List` to hold the value `0`.

The syntax of this for loop probably looks very strange to you, but in fact it is not too different from what happens in Python using `range`. They syntax `for(Integer i = 0; i < 10; i++)` is exactly equivalent to the Python `for i in range(10)`. The first statement inside the parenthesis declares and initializes a loop variable `i`. The second statement is a Boolean expression that is our exit condition. In other words, we will keep looping as long as this expression evaluates to true. The third statement is used to increment the value of the loop variable at the end of iteration through the loop. The syntax `i++` is C# shorthand for `i + 1`. C# also supports the shorthand `i--` to decrement the value of `i`. Like Python, you can also write `i += 2` as shorthand for `i = i + 2`.

Try to rewrite the following Python for loops as C# for loops. We've provided you a place to do this in the `ForLoopPractice` project in the example code solution.

```python
# Python
for i in range(2,101,2)
    print(i)
```

```python
# Python
for i in range(1,100)
    print(i)
```

```python
# Python
for i in range(100,0,-1)
    print(i)
```

Consider the next segment:

```csharp
// C#
for (int j = 0; j < data.Length; j++) {
    int val = int.Parse(data[j]);
    count[val] = count[val] + 1;
}
```

We are iterating through the `data` array in order to update the number of occurences of each value.

The line `count[val] = count[val] + 1;` illustrates another important difference between Python and C#. Notice that while `count` is of type `List` we can still use the square bracket operator `[]` to retrieve a value from the list, just as we can with Python lists.

Let's consider the last loop in this program:

```csharp
// C#
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
// C#

```

The main difference between this example and the previous example is that we declare count to be an array of integers: `int[] count = {0,0,0,0,0,0,0,0,0,0};`. This syntax initializes an array directly. Notice that we use the square bracket notation to index into an array: `count[idx]`.

## Key/Value Data: Dictionaries

Just as Python provides the dictionary structure to allow us to store data as key/value pairs, C# also provides us a similar mechanism. Rather than the dictionary terminology, C# calls these objects Maps. There are multiple types of maps, but we'll focus only on the most general purpose map type: `HashMap`.

Let's stick with a simple frequency counting example, only this time we will count the frequency of words in a document. A simple Python program for this job could look like this:

```python
# Python
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
// C#

```

As an exercise, see if you can improve the program above to ignore punctuation.

## References

- [List (msdn.microsoft.com)]()
- [Dictionary (msdn.microsoft.com)]()
- [Array (msdn.microsoft.com)]()
