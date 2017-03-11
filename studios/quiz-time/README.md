---
title: 'Studio: Quiz Time!'
currentMenu: studios
---

For this studio, you will design and build a program that allows the user to take a quiz. This means you will have to create some questions, and get some input from the user.

First, the questions. We want to be able to handle multiple types of questions:
- Multiple choice: a question with a fixed set of possible answers, of which only one may be chosen
- Short answer: a question with a freeform text answer
- Checkbox: a question with a fixed set of possible answers, of which any number may be chosen

## Design

In order to design your program, consider:

* What do these types of questions have in common?
* What makes these question types different?

Design a base class (called `Question`) that contains the common features, and design subclasses as necessary. For each, specify:
- Class name
- Parent class (if applicable)
- Fields, properties, and methods along with access modifiers

Should any of these questions be abstract? If so, should any of the methods of the abstract class be abstract?

Make sure that there is functionality included to display the questions, the choices (if necessary) and check to see if the answer is correct.

## Implementation

Code the classes that you designed above. If you like, get some feedback on your design by talking through it with a classmate.

## Putting it all together

You're now ready to present these questions as a Quiz. Use your classes in a `Main` method  within the `Program.cs` file of the project. The program should create several questions, present them to the user, accept the user's responses, and then tell them whether their answers were correct or incorrect.

## Bonus Mission

1. Add validation behavior to your `ShortAnswer` class to only allow the user to enter text with less than 80 characters.
2. Add a couple of more question types to your program:
    - Linear scale: a question that allows the user to provide a numeric response within an integer scale, which may vary from question to question. For instance, it could be 1-3 for on linear scale question, and 1-5 for another.
    - Paragraph: Similar to short answer, but allows for responses up to 500 characters.
