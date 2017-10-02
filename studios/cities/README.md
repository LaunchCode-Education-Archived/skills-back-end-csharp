---
title: 'Studio: Cities'
currentMenu: studios
---

This studio has some starter code. So let's get it set up first. You might enjoy [some music](https://www.youtube.com/watch?v=jJMxwBmQWHA) while you do so.

## Getting Ready

Set up a local copy of the project:
- Visit the [repository page](https://github.com/LaunchCodeEducation/Cities) for this project and fork the repository to create a copy under your own GitHub account.
- From within Visual Studio, choose the *Team Explorer* tab near the bottom of the *Solution Explorer* pane. If you don't see this tab, you can open it via the application menu: *View > Team Explorer*.
- Click on the *Manage Connections* icon (see below), and select *Clone* from the GitHub section of the *Team Explorer* and select your `Cities` copy from the modal window. **Be sure to change the Path field** to the location at which you would like the project to live, ideally inside of a folder you've been using to store other projects.
- Open the solution via either the notification within *Team Explorer* or via *File > Open > Project/Solution*.

## Cities Project Overview

The project contains a data file, `city_data.csv`, that contains data on over 300 U.S. cities. It has columns representing name, state, population (from the 2010 census) and land area (in square miles).

There is also a `City` class. This class encapsulates the same properties contained in our data file, along with providing a couple of methods to make printing info about cities easier.

The class `CityDataImporter` has a static `LoadData` method that opens the data file and parses it, returning a list of `City` objects.

Within `Program.cs`, we load the data, sort the list of `City` objects by the `City.Name` property, and print it out. Here's part of that code:

```csharp
List<City> cities = CityDataImporter.LoadData();

IComparer<City> comparer = new NameComparer();

cities.Sort(comparer);
```

To sort the `cities` list, we use `NameComparer`, which is located in the `Comparers/` folder and namespace of the project. `NameComparer` implements `IComparer<City>` by providing the `Compare(City, City)` method. Since sorting by `Name` is just sorting alphabetically by name, we use the `string.Compare(string, string)` method with the `Name` properties of the given input parameters.

The `IComparer<T>` interface contains one method: `Compare(T, T)`. It returns an integer which determines which of the two objects comes "before" (in other words, "is less than") the other. If the integer is less than zero, then the first parameter comes before the second. If the integer is zero, then they are "the same". If the integer is greater than zero, then the second parameter comes before the first. You can think of the result of calling `Compare(x, y)` as being the "value" of subtracting `x - y`. If `x` is smaller than `y`, this value is negative, if `x` is larger than `y`, this value is positive.

In order to sort the list, the comparer object is passed in to the `Sort` method for it to use. The list is sorted "in place". In other words, rather than returning a new list that is sorted, `Sort` sorts the given list by reordering its contents (i.e., the original list is mutated).

## Your Task

Your task is to implement at least two of the following comparers:

- `StateComparer` - results in alphabetical sorting by state
- `PopulationComparer` - results in sorting by population, from largest to smallest
- `AreaComparer` - results in sorting by land area, from largest to smallest

Your comparers should be placed in the `Comparers/` folder, and they should implement `IComparer<City>`. Test them out by modifying the code in `Program.cs`.

Refer to `NameComparer` and the [IComparer<T> documentation](https://msdn.microsoft.com/en-us/library/8ehhxeaf(v=vs.110).aspx) for guidance.

## Bonus Mission

Create a `CompoundComparer` class that is able to order based on multiple factors. For example, we should be able to order by state name alphabetically, and then by population.

Here are the steps to carry this out:

1. Create a class that implements `IComparer<City>`.
2. Create a property `Comparers` of type `IList<IComparer<City>>`.
3. Initialize `Comparers` to be an empty list: `new List<IComparer<City>>()`. You can do this in a constructor, or in the same line that you declare the property.
4. You'll need the following method in order to implement the interface:

    ```csharp
    public int Compare(City x, City y)
    ```

    This method should use each of the comparers in `Comparers` in order. You'll first use `Comparer[0]` to compare `x` and `y`.

    You only need to move on to the next comparer if the first comparer returns 0. For example, if you're comparing cities by state and then by population, when comparing St. Louis and New York, you don't need to compare population. You know that St. Louis comes before New York because "Missouri" comes before "New York". However, when comparing St. Louis and Kansas City, you would need to compare population, since the cities are in the same state.

    We suggest using a `while` loop to do this.
5. To use `CompoundComparer`, create an instance of the class and then add individual comparers in the order that want them to be used:
    ```csharp
    CompoundComparer comparer = new CompoundComparer();
    comparer.Comparers.Add(new StateComparer());
    comparer.Comparers.Add(new PopulationComparer());
    ```
