---
title: Class 7 Prep Exercises
currentMenu: classes
---

- **Controller inheritance:** When creating controllers in our MVC applications, we were required to extend the `Controller` class. [Explore the Controller class documentation](https://docs.microsoft.com/en-us/aspnet/core/api/microsoft.aspnetcore.mvc.controller), and look for methods that you've used within your own controllers.
    - If you wanted to override a method of `Controller` so that every time you rendered a view, `ViewBag.SiteTitle = "My MVC App"` was executed, which method would you override?
    - For this method, would you be allowed to override it? That is, is it declared `virtual`?
- **Class design:** Pick one or more of the following groups of classes, and diagram your design for each (including methods and properties). Be sure to use lines and arrows to indicate inheritance relationships, and to include data and behavior that somebody using your classes would likely want.
    - Shape, Square, Rectangle, Circle
    - Computer, Desktop, Laptop, SmartPhone
    - Student, GraduateStudent, UndergraduateStudent
- **Class implementation:** For one of the groups of classes above, implement your design and test it in a `Program.cs` class.
- **Abstract class design:** Consider the group of classes that you designed. Suppose you had a web program that used these classes, and you needed to assign a unique ID to every object created from one of these classes within the application. In other words, each such class should have an `Id` property, and no two objects created from any of the classes may have the same ID value. Create an abstract class, `AbstractEntity`, that contains the behavior for assigning and accessing such a unique ID for each class that extends it. Add this class to your program above, and add `AbstractEntity` to the class hierarchy in the correct place.
