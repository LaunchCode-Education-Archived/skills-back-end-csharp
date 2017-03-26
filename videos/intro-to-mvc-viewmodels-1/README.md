---
title: "Intro to ASP.NET Core MVC: ViewModels and Validation"
currentMenu: videos
---

<div class="youtube-wrapper"><iframe width="560" height="315" src="https://www.youtube.com/embed/kLLBDsPUoyY" frameborder="0" allowfullscreen></iframe></div>

## Errata

In the video it is stated that `using` statements are not allowed in Razor templates. This is not correct. You may add such statements using the following syntax.

```nohighlight
@using CheeseMVC.Models
@model List<Cheese>
```

This has the same effect as the following `@model` declaration, which was used in the video.

```nohighlight
@model List<CheeseMVC.Models.Cheese>
```

## Code

We start this lesson with the code in the `video-viewmodels-start` branch of the CheeseMVC repo: [starting code](https://github.com/LaunchCodeEducation/CheeseMVC/tree/video-viewmodels-start)

We end this lesson with the code in the `video-viewmodels-end` branch of the CheeseMVC repo: [ending code](https://github.com/LaunchCodeEducation/CheeseMVC/tree/video-viewmodels-end)

## References

* [Tag Helpers](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms)
* [Model Validation](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation)
