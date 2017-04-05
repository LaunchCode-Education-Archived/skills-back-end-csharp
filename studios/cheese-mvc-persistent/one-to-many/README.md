---
title: 'Studio: CheeseMVC - Persistent (One-to-Many)'
currentMenu: studios
---

This continues the guided studio in which we set up `CheeseMVC` to work with EntityFramework. If you've completed [Part I: Single Class Persistence](../single-class-persistence/) then you're ready to begin this activity.

## Add Cheeses to CheeseCategory

Also give the class a `Cheeses` property of type `IList<Cheese>`.

## Replace CheeseType with CheeseCategory

Up until now, we've been using the enum class `CheeseType` to represent the type of cheese that the user may choose from. This isn't very flexible, however, as the user can't create new types. For a new type to be added to the application, the `CheeseType` enum class must be changed, which requires editing code, of course.

Using the `CheeseCategory` class to categorize cheese objects will be much more flexible. Users will be able to create new categories themselves.

Within `Cheese`, replace the `Type` property with a property named `Category` and of type `CheeseCategory`. Also add an integer `CategoryID` property. It's important for these two properties to be named in this related way for EntityFramework to recognize the integer as the property corresponding to the `ID` of the `Category` when mapping classes.

When we retrieve a `Cheese` object from the database, both the `Category` and `CategoryID` properties will be properly initialized, and the value of `CategoryID` will be the value of the `ID` property of `Category`. In other words, `CategoryID` is a foreign key property.

<aside class="aside-warning" markdown="1">
There are additional ways to set up relationships between classes so that EF properly manages the relationship. When getting started with EF, it can be easier to stick to one convention until you're comfortable with the framework, and then expand your knowledge.

If you're curious, you can [read more about mapping relationships](https://docs.microsoft.com/en-us/ef/core/modeling/relationships), and other ways that these can be set up properly to work with EF.
</aside>
