---
title: Class 4 Prep Exercises
currentMenu: classes
---

Get some hands-on practice with views in MVC. Work on these exercises within the `CheeseMVC` app that was created during [part 1](../../videos/intro-to-mvc-views-1/) and [part 2](../../videos/intro-to-mvc-views-2/) of our Intro to MVC Views lessons.

1. Add a `description` field to the application. This will involve:
    - Modifying the static `cheeses` list to be a dictionary with key/value pairs that correspond to the name and description.
    - Adding a new form field in `Cheese/Add.cshtml` to allow for submission of the description.
    - Modify the `NewCheese` action to insert the description of the new cheese into the `cheeses` dictionary.
    - Display the description field in the `Cheese/Index.cshtml` view template.
2. Use `_Layout.cshtml`. In other words, remove `Layout = null` from the top of the templates, and modify `_Layout.cshtml` to reflect links for the CheeseMVC app (only Home and Add for now).
