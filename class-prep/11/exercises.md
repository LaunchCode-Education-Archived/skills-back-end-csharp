---
title: Class 11 Prep Exercises
currentMenu: classes
---

Complete these coding exercises and research questions.

1. We know that the `List<T>` class implements the `IList<T>` interface, and we've also learned that we can put a `List<T>` in a variable of type `IList<T>`, and that it's good to declare variables and parameters to be interface types whenever possible.  Compare the documentation for [List<T>](https://msdn.microsoft.com/en-us/library/6sh2ey19(v=vs.110).aspx) and [IList<T>](https://msdn.microsoft.com/en-us/library/5y536ey6(v=vs.110).aspx) and find at least one situation in which you would need to use a variable or parameter specifically of type `List<T>`, rather than just `IList<T>`. In other words, what's something that a `List<T>` can do that an `IList<T>` can't do?
1. We've learned that `List<T>` implements both `IList<T>` and `IEnumerable<T>`. In fact, `IList<T>` extends `IEnumerable<T>`, so that `IList<T>` includes all of the contracted methods that `IEnumerable<T>` does.

    Open up your `TechJobsMVC` solution. Within `ListController` and `SearchController`, change every local variable that's declared to be of type `List` to be either an `IList` or an `IEnumerable`, using the least restrictive type as possible. In other words, if you only need to loop over the collection, use `IEnumerable`, but if you also need to access elements of the collection by index -- as in, `var item = items[0]` -- then use `IList`. Be sure to look at the templates to see how collections being passed into the templates are used. Also be sure to test your code after making changes!
1. In our action methods in MVC apps, we've been returning objects of type `IActionResult`. As you might guess, given the leading `I`, this is an interface type! Answer the following questions, using documentation for [IActionResult](https://docs.microsoft.com/en-us/aspnet/core/api/microsoft.aspnetcore.mvc.iactionresult) and the [Microsoft.AspNetCore.Mvc namespace](https://docs.microsoft.com/en-us/aspnet/core/api/microsoft.aspnetcore.mvc):
    - What behavior(s) are part of the `IActionResult` interface?
    - Which class implements the `IActionResult` result?
    - Find at least 3 classes that extend the class from the last question, including some that you've used.
