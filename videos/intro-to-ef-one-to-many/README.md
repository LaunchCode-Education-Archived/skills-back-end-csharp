---
title: "Intro to EntityFrameworkCore: One-to-Many Relationships"
currentMenu: videos
---

<aside class="aside-warning" markdown="1">
In this video and others, we use Powershell to run migration commands. As of mid-2017, these migration command-line tools are only compatible with the cmd.exe command prompt, and *not* Powershell. Thus, whenever we type `powershell` in the location bar, you should instead type `cmd` to open the proper command line tools.
</aside>

<div class="youtube-wrapper"><iframe width="776" height="437" src="https://www.youtube-nocookie.com/embed/bFbb8Wetq2o?rel=0" frameborder="0" allowfullscreen></iframe></div>

## Notes

In this lesson we'll look at how to structure persistent model objects that have relationships with each other. In particular, we'll look at one-to-many relationships. "One-to-many relationships" describe classes that can have many instances of another class.

In our `CheeseMVC` application, an example of this is the relationship between the `Cheese` class and the `CheeseCategory` class. Each `CheeseCategory` may have many `Cheese` objects related to it. To manage this relationship, we've added two new properties to our `Cheese` class:

```csharp
public int CategoryID { get; set; }
public CheeseCategory Category { get; set; }
```

The `CategoryID` property acts as a foreign key and the `Category` property is a navigation property, meaning it is the property that corresponds to that particular `CategoryID`.

For a more detailed walkthrough of creating the code in this video, review Parts 1-3 of the [CheeseMVC Persistent studio](http://education.launchcode.org/skills-back-end-csharp/studios/cheese-mvc-persistent/).

## Code

You'll create the code featured in this lesson yourself as part of the CheeseMVC Persistent studio (which doubles as your final assignment)!

## References

- [Relationships In EF Core](https://docs.microsoft.com/en-us/ef/core/modeling/relationships)
