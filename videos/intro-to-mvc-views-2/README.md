---
title: "Intro to ASP.NET Core MVC: Views (Part 2)"
currentMenu: videos
---

<div class="youtube-wrapper"><iframe width="776" height="437" src="https://www.youtube-nocookie.com/embed/4xvSOmGxyKQ?rel=0" frameborder="0" allowfullscreen></iframe></div>

## Notes

<aside class="aside-warning" markdown="1">
When running the `CheeseMVC` application, your data will "disappear" each time you restart your app. This is because storing data in C# data structures only preserves that data while the application is running; this data only exists in-memory. We'll look at persisting data in a more permanent way in future lessons.
</aside>

In our *CheeseMVC* application we are going to create a main page that displays a list of cheeses and descriptions of those cheeses, and also an add page where users can add a cheese and its description. Be sure to code along with the video. These notes only include some of the code featured in the video.

An example of working with C# syntax in a view file is looping through and displaying a list of cheeses in a Razor template. To do so, precede the C# code with an `@` symbol. For example:

```nohighlight
<ul>
  @foreach (string cheese in cheeses)
  {
    <li>@cheese</li>
  }
</ul>
```

After moving the list data to the controller, you can modify the `foreach` like so:
```nohighlight
@foreach (string cheese in ViewBag.cheeses)
```

To add a link to the add page from the index page, add this to the `Index.cshtml`:

```nohighlight
<p><a asp-controller="Cheese" asp-action="Add">Add Cheese</a></p>
```

### ViewBag and ViewData

In addition to using `ViewBag` to pass data from an action method to a view, you can use the `ViewData` dictionary. To set data in `ViewData` in the controller, use:

```csharp
ViewData["cheeses"] = cheeses;
```
And to retrieve it in the view, just add `@`:
```nohighlight
@ViewData["cheeses"]
```

The `ViewBag` and the `ViewData` objects use the same underlying data structure, so you can add data to the `ViewBag` and then retrieve it from `ViewData` (and vice versa). We'll most often use `ViewBag` in this course.

## References

- [Razor Syntax (docs.microsoft.com)](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/razor)
- [Razor Syntax Cheatsheet](https://gist.github.com/jonlabelle/8738373)
