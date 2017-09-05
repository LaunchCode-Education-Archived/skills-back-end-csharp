---
title: 'Studio: CheeseMVC Persistent'
currentMenu: studios
---

## Part 2: Setting Up a One-to-Many Relationship

This continues the guided studio in which we set up `CheeseMVC` to work with the EntityFramework. If you've completed [Part 1: Single Class Persistence](../single-class-persistence/) then you're ready to begin this activity.

If you get stuck on any of the steps here refer to the video lessons. You'll often find the answers there.

## Add Cheeses to CheeseCategory

Within `CheeseCategory`, add a `Cheeses` property of type `IList<Cheese>`. After we set up the `Cheese` class to work with `CheeseCategory` objects, this list will represent the list of all items in a given category. We'll do this in a bit.

## Replace CheeseType with CheeseCategory

Up until now, we've been using the enum class `CheeseType` to represent the type of cheese that the user may choose from. This isn't very flexible, however, as the user can't create new types. For a new type to be added to the application, the `CheeseType` enum class must be changed, which requires editing code, of course.

Using the `CheeseCategory` class to categorize cheese objects will be much more flexible, as it will allow users to create new categories themselves.

Within `Cheese`, replace the `Type` property with a property named `Category`, of type `CheeseCategory`. Also add an integer `CategoryID` property. It's important for these two properties to be named in this related way for EntityFramework to recognize `CategoryID` as the property corresponding to the `ID` of the `Category` property when mapping classes.

When we retrieve a `Cheese` object from the database, both the `Category` and `CategoryID` properties will be properly initialized, and the value of `CategoryID` will be the value of the `ID` property of `Category`. In other words, `CategoryID` is a foreign key property.

<aside class="aside-warning" markdown="1">
There are additional ways to set up relationships between classes so that EF properly manages the relationship. When getting started with EF, it can be easier to stick to one convention until you're comfortable with the framework, and then expand your knowledge.

If you're curious, you can [read more about mapping relationships](https://docs.microsoft.com/en-us/ef/core/modeling/relationships), and other ways that these can be set up properly to work with EF.
</aside>

Delete the `CheeseType` class by right-clicking on `CheeseType.cs` in the Solution Explorer and selecting *Delete*. This will create compiler/build errors where this type is used, but we're about to fix them!

## Updating the ViewModel

Now that our `Cheese` objects can have a `CheeseCategory`, let's update the rest of our code to make use of this.

Open up `AddCheeseViewModel`, and remove the `Type` and `CheeseTypes` properties. Add these properties in their place:

```csharp
[Required]
[Display(Name = "Category")]
public int CategoryID { get; set; }

public List<SelectListItem> Categories { get; set; }
```

Update the ViewModel constructor to accept a parameter: `IEnumerable<CheeseCategory> categories`. This will be passed in when we create a new `AddCheeseViewModel` in the controller, and will be a collection of all categories. This is the best way for our ViewModel to get such a list, since it can only be obtained via the `CheeseDbContext`, which our controller has a reference to.

Add an empty default constructor. Since we modified the existing constructor to no longer be a no-arg (aka default) constructor we need to add one so that model binding will work.

Update the code in the controller to correctly populate the `Categories` property based on the changes we made. You can mimic the code that's there for the old `CheeseType` enum. When creating a new `SelectListItem`, the `Value` property should receive a category ID, and the `Text` property should receive the name of the category.

## Updating CheeseController

Open up `CheeseController`. We'll make several updates here.

### Index

Modify the call to retrieve all `Cheese` objects to be:

```csharp
IList<Cheese> cheeses = context.Cheeses.Include(c => c.Category).ToList();
```

This will ensure that when each `Cheese` object is retrieved from the database, its `Category` is retrieved as well.

### Add

Update the creation of the `AddCheeseViewModel` to pass the collection of all category objects into the constructor. You can retrieve this collection by calling `context.Categories.ToList()`.

### Add (HttpPost)

This action creates a new cheese. Based on our updates to `AddCheeseViewModel`, the ViewModel passed in will have a `CategoryID` property representing the category that the user selected for their new cheese.

We'll need to have the `CheeseCategory` object corresponding to this ID, so we can set up the new cheese properly.

```csharp
CheeseCategory newCheeseCategory =
                    context.Categories.Single(c => c.ID == addCheeseViewModel.CategoryID);
```

This will fetch a single `CheeseCategory` object, with ID matching the `CategoryID` value selected.

You should now update the creation of the `newCheese` object to set the `Category` property to be the category that we just retrieved.

## Updating the View(s)

### Views\Cheese\Add.cshtml

Open this view template, and update the form to use the `Categories` list that's part of `AddCheeseViewModel`. This will entail updating the element in the final form group, so that it's no longer referencing the old code that used enum types, and instead creates the select list using `Model.Categories`.

### Views\Cheese\Index.cshtml

Update the table to display the category name of a given cheese instead of its type. Update the header as well, so it has "Category" in place of "Type".

## Test!

You made a lot of changes, so you might want to make sure you don't have any build errors: run *Build > Build Solution*.

Assuming that looks good, start up your application. Make sure you can create a new cheese object, selecting a pre-existing category. Then make sure the proper category name is displayed in the table on the home page after doing so.

When everything works, move on to [Part 3](../many-to-many/).
