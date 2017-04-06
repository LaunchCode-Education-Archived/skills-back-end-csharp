---
title: "Intro to EntityFrameworkCore: Persisting Objects"
currentMenu: videos
---

If you haven't completed the [EF Core setup steps](../../class-prep/12/setup.html) for `CheeseMVC`, go back and do so before watching this lesson.

<div class="youtube-wrapper"><iframe width="560" height="315" src="https://www.youtube.com/embed/MxUOP2NPiEo" frameborder="0" allowfullscreen></iframe></div>

## Notes

### App Setup

These are the code sections referenced in the video that were part of the starter code. Namespace and using statements are omitted.

**Data\CheeseDbContext.cs**

```csharp
public class CheeseDbContext : DbContext
{

    public DbSet<Cheese> Cheeses { get; set; }

    public CheeseDbContext(DbContextOptions<CheeseDbContext> options)
        : base(options)
    {
    }
}
```

In **Startup.cs** within the `ConfigureServices` method:

```csharp
services.AddDbContext<CheeseDbContext>(options =>
    options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
```

The `"DefaultConnection"` refers to the database connection string in `appsettings.json`, which you set up in the [previous tutorial](../../class-prep/12/setup.html).

### Migrations

To create a new migration after making changes to your model, right-click on the project in the Solution Explorer and select *Open Folder in File Explorer*.

<img alt="Open Folder in File Explorer" src="images/open-folder.png" style="width:500px;" />

This opens File Explorer to the top-level directory of the project.

Within the File Explorer window, click on the far-right end of the Location field, and type `powershell`. Hit Enter.

![powershell](images/powershell.png)

This opens a Powershell with the path already set to the current directory. From this location, you can run .NET Tools commands.

#### New Migration

To add a migration:

```nohighlight
> dotnet ef migrations add MigrationName
```

Use a different and descriptive name for each migration.

#### Update Database to Latest Migration

```nohighlight
> dotnet ef database update
```

#### Change State to a Specific Migration

To update the database to a specific migration -- either forward or backward from the current state -- run:

```nohighlight
> dotnet ef database update MigrationName
```

#### Remove a Migration

If you create a migration and later realize you don't want the associate changes, you can remove it. To remove a migration:

```nohighlight
> dotnet ef migrations remove MigrationName
```

If you haven't done so already, you must first undo the given migration.

#### Undo All Migrations

```nohighlight
> dotnet ef database update 0
```

<aside class="aside-pro-tip" markdown="1">
If you wish to start with a clean database during development -- because, let's be honest, sometimes we'll break something or want to undo a bunch of work -- perhaps the easiest thing to do is change the database name in the connection string in `appsettings.json`. Then you can run `dotnet ef update database` and a new, empty database will be set up with all migrations run.
</aside>

## Code

We start this lesson with the code in the `video-ef-basics-start` branch of the CheeseMVC repo: [starting code](https://github.com/LaunchCodeEducation/CheeseMVC/tree/video-ef-basics-start)

We end this lesson with the code in the `video-ef-basics-end` branch of the CheeseMVC repo: [ending code](https://github.com/LaunchCodeEducation/CheeseMVC/tree/video-ef-basics-end)

## References

* [DbContext Class](https://docs.microsoft.com/en-us/ef/core/api/microsoft.entityframeworkcore.dbcontext#Microsoft_EntityFrameworkCore_DbContext)
* [.NET Command Line Tools](https://docs.microsoft.com/en-us/ef/core/miscellaneous/cli/dotnet)
