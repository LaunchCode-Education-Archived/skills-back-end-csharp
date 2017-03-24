---
title: 'Studio: User Signup'
currentMenu: studios
---

For this studio you will create an MVC application with functionality that allows users to "sign up" for your app.

## Getting Ready

Create a new ASP.NET Core Web Application within Visual Studio named `UserSignup`.
- Create a `UserController` in `Controllers/`
- Create a new folder, `User/`, within `Views/`
- Create `Index.cshtml` and `Add.cshtml` templates within`Views/User`
- Create a `Models` folder and within that folder a `User` class

## Creating the Model

Your `User` class should have a few public properties: `Username`, `Email`, `Password`. These should each be strings.

If you create a non-default constructor, be sure to also create a default constructor (which can be empty).

## Rendering the Add User Form

Within `UserController`, create an `Add` action to render the form. Within the `Add.cshtml` template, create a form that accepts inputs for each of the `User` properties, along with a Verify Password input. The password and verify inputs should have `type="password"`.

The form should be set up to `POST` to the same URL that it is displayed at.

## Handling Form Submission

Within the controller, create an action `Add(User user, string verify)`. This will use model binding to create a new user object, `user`, and pass it into your action method. Check that `verify` matches the password within the `user` object. If it does, render the `Index.cshtml` view template with a message that welcomes the user by name.

If the passwords don't match, render the form again with the username and email fields already populated, along with a message indicating what went wrong.

<aside class="aside-warning" markdown="1">
If one of the password fields is left blank, that property or parameter will be `null`. You'll need to handle this appropriately.
</aside>

You don't need to store the `User` object anywhere. We're focusing on form handling and validation in this exercise. If you want to keep track of users using the method we employed in the models lesson video, check out the Bonus Missions below.

## Bonus Missions

1. Add a `UserId` property to `User`, and create a `UserData` class within `Models/` that provides access to a list of users via `Add`, `GetAll`, and `GetById`.
1. Add additional validation within `UserController.Add(User user, string verify)` to make sure that the username and email are not empty, that the username is between 5 and 15 characters long, and the username contains only letters. If any of these checks fails, render the form again with an appropriate message. When doing so, make sure that any inputs that *did* validate are populated with the value the user provided the first time.
1. This builds on 1. In the `User/Index.cshtml` view, display a list of all users by username. Each username should have a link that takes you to a detail page that lists the user's username and email.
1. Add a `DateTime` property in `User`, and initialize it to the time the user joined (i.e. when the `User` object was created). Display the value of this property in the user detail view.
