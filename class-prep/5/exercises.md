---
title: Class 5 Prep Exercises
currentMenu: classes
---

1. **Class Design:** In Visual Studio, create a new console project named `School` in the `csharp-exercises` solution that has the class `Student` that was discussed in [the reading for this class][encapsulating-data]. Add the properties that we looked at, and think about the access level each should have. Reduce the access level of at least one setter to less than public. Make sure you can defend the reasoning behind your choice.
1. **More class design:** In the `School` project, create a class named `Course` with at least three properties. Before diving into Visual Studio, use pen and paper to work through what these might be, including the data type, access level, and whether it makes sense for any of them to be readonly or constants. At least one of your fields should be a `List` or `Dictionary`, and you should use your `Student` class.
1. **More Cheese:** More CheeseMvc, that is. Fire up this MVC application, and create a new folder at the same level of `Controllers/` and `Views/` named `Models`. Within that folder, create a `Cheese` class that has `Name` and `Description` properties. Refactor the code in your `CheeseController` to use `Cheese` objects rather than the strings that were used previously. You'll need to update your views as well.
1. **Review:** With a pen and paper, write down descriptions of each of the following field types, along with an example of a situation where you might use each: public field/property, private field, static field/property, readonly field/property. If you get stuck, review the lesson on [encapsulating data][encapsulating-data].


[encapsulating-data]: ../../csharp4python/classes-and-objects-encapsulating-data/
