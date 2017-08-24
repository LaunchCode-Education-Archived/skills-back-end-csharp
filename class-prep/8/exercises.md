---
title: Class 8 Prep Exercises
currentMenu: classes
---

Add edit functionality to the `CheeseMVC` application by following these steps. Make sure you've added all of the code from the [models lesson](../../videos/intro-to-mvc-models/).

1. Add two action methods to `CheeseController`. Just stub them out for now; we'll implement the code to make them work in a minute.
    - An action method to display the form:
        ```csharp
        public IActionResult Edit(int cheeseId)
        ```
    - An action method to process the form:
        ```csharp
        public IActionResult Edit(int cheeseId, string name, string description)
        ```
1. Add the `[HttpPost]` attribute to the second result.
1. Create an `Edit.cshtml` view template in `Views/Cheese/`.
1. Copy the form from `Add.cshtml` into `Edit.cshtml`. You'll want everything between and including the `<form>` tags.
1. Back in the `Edit(int id)` action, ask `CheeseData` for the object with the given `cheeseId` and put it in the `ViewBag`.
1. Within the form fields in `Edit.cshtml`, get the name and description from the cheese that was passed in via the `ViewBag` and set them as the values of the form fields.
1. Add another input to hold the id of the cheese being edited. This should be hidden from the user:
    ```html
    <input type="hidden" value="@ViewBag.cheese.CheeseId" name="id" />
    ```
1. Add a heading at the top of `Edit.cshtml` that says "Edit Cheese NAME (id=ID)" where NAME and ID are replaced by the values of the given cheese.
1. Back in the `Edit(int id, string name, string description)` action, query `CheeseData` for the cheese with the given id, and then update its name and description. Redirect the user to the home page.
1. In `Views/Cheese/Index.cshtml`, add a link to edit the cheese:
    ```html
    <a asp-controller="Cheese" asp-action="Edit" asp-route-id="@cheese.CheeseId">edit</a>
    ```
    You can put this link in a third table column, or in one of the existing table cells.
1. Test your code! With so many changes, it's not unlikely that you've made an error somewhere. Be patient, use the Visual Studio debugger, and read your error messages.
