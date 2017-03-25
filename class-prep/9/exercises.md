---
title: Class 9 Prep Exercises
currentMenu: classes
---

1. Let's use a ViewModel in our `Edit` action methods. If you don't have edit functionality already, you can add it by following the steps in [class 8 prep exercises](../8/exercises.html). Change the name of this class to `AddEditCheeseViewModel` to more properly reflect its use.

    This ViewModel will need most of the same properties and methods as `AddCheeseViewModel`, so create a ViewModel class that extends `AddCheeseViewModel`. The only property you'll need to add right now is a `CheeseId` property to hold the ID of the cheese being edited.

    After creating the ViewModel, use it in both `Edit` actions. Since you'll be populating the form with the data from an existing cheese, you'll need to initialize the `CheeseId` in the `Edit` action that displays the form.

1. Add an integer property to `Cheese` to allow the user to give each cheese a rating. Follow these steps:
    - Add the property to `Cheese.cs`
    - Add the property to `AddCheeseViewModel`
    - Add the form input and label to `Views/Cheese/Add.cshtml`
    - In the `CheeseController.Add` action that handles form submission, create the new cheese with the rating
    - Display the rating in `Views/Cheese/Index.cshtml`
    - Add validation in the ViewModel to ensure the rating is within a proper range, say 1-5. Refer to the [validation attributes overview](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation#validation-attributes) for options on doing this.
1. Within `AddCheeseViewModel` create a method `CreateCheese` that returns a `Cheese` object that has been created using the properties of `AddCheeseViewModel`. Refactor `CheeseController.Add` (the one that processes the form) to use this method, rather than creating a `Cheese` object directly. This encapsulates this functionality in the ViewModel, and makes the code more reusable.
