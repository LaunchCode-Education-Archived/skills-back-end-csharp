---
title: "Intro to ASP.NET Core MVC: Views (Part 1)"
currentMenu: videos
---

<div class="youtube-wrapper"><iframe width="776" height="437" src="https://www.youtube-nocookie.com/embed/H2Nf0w-YKcE?rel=0" frameborder="0" allowfullscreen></iframe></div>

## Notes

In this video we look at views and the Razor Template Engine. Be sure to code along with the video. These notes only include some of the code featured in the video.

<aside class="aside-note" markdown="1">
Note that at around 5:40 in the video, we say "the default controller and the default action are **Hello** and Index", but what we should have said is that they are "**Home** and Index".
</aside>

The `View()` method finds a template that's associated with the particular controller and action method that it is called from.

Within the `Views` folder, there will be a folder corresponding to each controller. This folder will contain the templates for each action method in that controller.

Razor templates are a mixture of C# and HTML. The C# code is enclosed within `@{}` To create a folder for a new controller and to create a razor template do the following:
* Right-click on the `Views` folder and select *Add->New Folder*. Name the folder `Cheese` so that it corresponds to your new controller.
* Then right-click on the `Cheese` folder and select *Add->New Item->MVC View Page*. You can leave the name, `Index.cshtml`, as is. In the future, if you are creating a template for a different method action, you would rename it to match the method action name.

The header and footer that appear are provided by the `_Layout.cshtml` file found in your `Shared` folder. If you do not want to use this file, you can put `Layout = null;` in your template within the `@{}`.

Note that when you make changes to your templates, you can just refresh the browser to see those changes. But when you make changes to your controller, you have to stop and restart the application.

To override the default behavior of the `View()` method and have it look for a template with a different name than that of the action method, you can pass in a parameter which is the name of the template you want to render. E.g., `return View("Error");`.
