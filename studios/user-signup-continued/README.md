---
title: 'Studio: User Signup Continued'
currentMenu: studios
---

We'll build on the [User Signup](../user-signup/) studio from last class, adding in a ViewModel and validation.

## Getting Started

Open up your `UserSignup` application from last time, and create a `ViewModels/` folder at the same level as `Models`. Within this folder, create a `AddUserViewModel`.

Add some properties to this new ViewModel. The ViewModel will be used in the view and actions that display and process the form, so think about what these properties should be. You'll need the properties necessary to create a new user, but you'll need more than that for the form.

## Add Validation Attributes

Add [validation attributes](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation#validation-attributes) to the properties in the ViewModel. You will have a property named `Verify` (or something similar). For its validation, it should match the `Password` property, so use the validation attribute `[Compare("Password")]`.

## Using the ViewModel in the Controller

Within both `Add` actions in the `UserController`, use the new ViewModel class to both pass data into, and receive data from the form. Upon form submission, you'll want to check that the model is valid using `ModelState.IsValid`, but you'll also need to check that the password and verify password fields match, which won't be handled by the configured validation attributes.

If you're unsure about how to do this, revisit the [lesson on ViewModels](../../videos/intro-to-mvc-viewmodels-1/), along with the source code linked on that video lesson page.

<aside class="aside-warning" markdown="1">
If you did any of the Bonus Missions in the previous studio, you'll be tearing out some of that code, since we'll now have the framework handle validation.
</aside>

## Using the ViewModel in the View

Refactor `Add.cshtml` to use [tag helpers](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms) to render the form inputs. Also use the tag helpers for error message display, either for the entire form in a `div` with:

```html
<div asp-validation-summary="All"></div>
```

Or on a per-field basis with:

```html
<span asp-validation-for="PROPERTY"></span>
```

(where PROPERTY is a placeholder for the given property).

Don't forget to declare the ViewModel at the top of the view using the syntax:

```nohighlight
@model UserSignup.ViewModels.AddUserViewModel
```

## Test, Test, Test!

You made a lot of changes! Be sure to throughly test them to make sure everything works as expected.
