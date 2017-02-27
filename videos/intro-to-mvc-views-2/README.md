---
title: "Intro to ASP.NET Core MVC: Views (Part 2)"
currentMenu: videos
---

<div class="youtube-wrapper"><iframe width="560" height="315" src="https://www.youtube.com/embed/4xvSOmGxyKQ" frameborder="0" allowfullscreen></iframe></div>

## Notes

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
