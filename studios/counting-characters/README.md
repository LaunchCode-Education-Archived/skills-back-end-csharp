---
title: 'Studio: Counting Characters'
currentMenu: studios
---

Let's revisit the [Counting Characters studio](https://runestone.launchcode.org/runestone/static/thinkcspy/Studios/counting-characters.html) from unit 1 (you'll need to log into the Unit 1 site to view this page).

Write a program that calculates the number of times each character occurs in a string and prints these counts to the console. You could get the string as input from the user, but for the sake of simplicity, you may also hard-code the string into your program as the value of a variable. Here’s a test string, for your convenience:

```nohighlight
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc accumsan sem ut ligula scelerisque sollicitudin. Ut at sagittis augue. Praesent quis rhoncus justo. Aliquam erat volutpat. Donec sit amet suscipit metus, non lobortis massa. Vestibulum augue ex, dapibus ac suscipit vel, volutpat eget massa. Donec nec velit non ligula efficitur luctus.
```

Your approach to this problem should be the same as with Python: Loop through the string one character at a time, storing and/or updating the count for a given character using an appropriate data structure.

Some questions to ponder as you start this studio:
- Which type of data structure (`Dictionary`, `List`, or `Array`) should you use to store character counts?
- You'll need to "initialize" the counts for the characters in some fashion. It's probably better to do this as you go through the string, as opposed to doing so before you loop through the string. (Why?)

If you're having trouble recalling how to create a new class, revisit the instructions in [Studio: Area of a Circle](../area/). And don't forget to check out the [Bonus Missions](#bonus-missions) below.

For the example string above, your output should look something like:

```nohighlight
L: 1
o: 15
r: 9
e: 26
m: 11
 : 50
i: 27
p: 7
s: 29
u: 28
d: 4
l: 17
t: 29
a: 22
,: 4
c: 17
n: 14
g: 7
.: 8
N: 1
q: 3
U: 1
P: 1
h: 1
j: 1
A: 1
v: 4
D: 2
b: 3
V: 1
x: 1
f: 2
```

## Bonus Missions

Here are few ways you might modify your solution:

- Make the counts case-insensitive
- Exclude non-alphabetic characters
- Get the string as input from the user at the command line
- Read the string in from a file. *Note:* This is a hard one, and we won't talk about reading from files in C# in this course, so be ready for a tough challenge if you bite this one off.
