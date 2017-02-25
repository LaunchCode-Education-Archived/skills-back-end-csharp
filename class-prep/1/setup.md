---
title: Initial Setup
currentMenu: classes
---

The steps here will walk you through setting up a repository that you'll use to study example code, work on studios, and complete your first assignment of this unit.

## Visual Studio

Visual Studio is the Integrated Development Environment (IDE) used to develop C# and .NET applications.

### Windows Users

Visit the [Microsoft Free Developer Apps](https://www.visualstudio.com/free-developer-offers/) page and download Visual Studio Community.

When installing Visual Studio, select the option to Customize the install and be sure to check the GitHub Extension for Visual Studio check box. If you install Visual Studio without doing this -- or have a pre-existing intsall -- then you can add the GitHub extension after the fact by downloading and installing it from [visualstudio.github.com](https://visualstudio.github.com/).

<aside class="aside-warning" markdown="1">
If you installed Visual Studio previously on your Windows computer, you will likely need to install the .NET Core Tools package. To do so, follow the [instructions provided by Microsoft](https://www.microsoft.com/net/core#windowsvs2015).
</aside>

### Mac and Linux Users

If you installed the Windows 10 development image, then you already have everything you need.

## GitHub Project Setup

Visit the [LaunchCodeEducation/csharp-exercises](https://github.com/LaunchCodeEducation/csharp-exercises) repository page and fork the repository into your own GitHub account by selecting *Fork* from the top right of the page.

After forking, open Visual Studio. From within Visual Studio, choose the *Team Explorer* tab near the bottom of the *Solution Explorer* pane. If you don't see this tab, you can open it via the application menu: *View > Team Explorer*. The first time you do this, you'll need to sign in to GitHub.

Once authenticated, select *Clone* from the GitHub section of the *Team Explorer* and select your `csharp-exercises` copy from the modal window. **Be sure to change the Path field** to the location you would like the project to live, ideally inside of a folder you've been using to store other projects.

VM (Mac/Linux) users: Don't forget to use the `lc101` directory within your Dropbox folder for this purpose.

## Configure and test

If your solution isn't open, open it via *File > Open > Project/Solution* and browse to the `.sln` file within the `csharp-exercises` directory.

Right-click on the top-level "Solution 'csharp-exercises'" item in the *Solution Explorer* and select *Properties*. In the modal that opens, select *Common Properties > Startup Project* and then choose *Current Selection* in the pane at the right.

<aside class="aside-pro-tip" markdown="1">
This setting makes the default behavior of Visual Studio to run the currently-selected program when you hit the <span style="color:green">▶︎</span> *Start* button in the toolbar.
</aside>
