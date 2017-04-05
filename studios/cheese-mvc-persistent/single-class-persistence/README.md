---
title: 'Studio: CheeseMVC - Persistent (Single Class Persistence)'
currentMenu: studios
---

Be sure you've completed the [setup steps](../) before starting these tasks.

## Setting Up the New Model

We'll use EntityFramework (EF) to create and object-relational mapping for a new class.

In `Models/`, create a new model class named `CheeseCategory`. Give it an `ID` property and a `Name` property that's a string.

We'll want instances of this class to be stored in the database, so open up `Data\CheeseDbContext` and add a new `DbSet`:

```csharp
public DbSet<CheeseCategory> Categories { get; set; }
```

<aside class="aside-note" markdown="1">
Once we add
</aside>

Since `Cheese` and `CheeseCategory` will be related (in Part II of this activity), we can put these `DbSet` properties in the same `DbContext`.

By naming this property `Categories`, EF will create a table within our database of the same name. This requires a

## Adding Categories

Create a `CategoryController` in `Controllers\`, and add the following code to the class:

```csharp
private readonly CheeseDbContext context;

public CategoryController(CheeseDbContext dbContext)
{
    context = dbContext;
}
```

This creates a private field `context` of type `CheeseDbContext`. This object will be the way in which we interact with objects stored in the database throughout our controller. You would need to add this code to each controller in which you wanted to be able to add or retrieve persistent objects managed by `CheeseDbContext`.

### View All Categories

Create an `Index` action within `CategoryController`, and the corresponding view template within the `Views` folder. You'll need to create `Views\Category\`.

The `Index` action should retrieve the list of all categories. This is done via `context`: `context.Categories.ToList()` returns a list of all `CheeseCategory` objects within the database.
