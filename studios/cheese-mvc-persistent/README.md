---
title: 'Studio: CheeseMVC Persistent'
currentMenu: studios
---

In this studio, you'll implement the functionality described in the video lessons on using EntityFrameworkCore.

## Getting Ready

Let's set up a new project for this studio. That way, everybody will start with the same code. If you've been working on CheeseMVC on your own, you should still do this. The instructions assume certain structure to your model classes and controllers.

Set up a local copy of the project:
- Visit the [repository page](https://github.com/LaunchCodeEducation/CheeseMVCPersistent) for this project and fork the repository to create a copy under your own GitHub account.
- From within Visual Studio, choose the *Team Explorer* tab near the bottom of the *Solution Explorer* pane. If you don't see this tab, you can open it via the application menu: *View > Team Explorer*.
- Click on the *Manage Connections* icon (see below), and select *Clone* from the GitHub section of the *Team Explorer* and select your `CheeseMVCPersistent` copy from the modal window. **Be sure to change the Path field** to the location at which you would like the project to live, ideally inside of a folder you've been using to store other projects.
	![Manage Connections](../../assignments/images/team-explorer-connections.png)
- Open the solution via either the notification within *Team Explorer* or via *File > Open > Project/Solution*.
- Pop back over to the *Solution Explorer* to preview the code.

<aside class="aside-note" markdown="1">
The code you are starting with has all of the correct packages and project settings need to enable EntityFrameworkCore. This means you *do not* need to walkthrough the setup steps that you carried out for [class 12 prep](../../class-prep/12/setup.html).
</aside>

## Getting Started

This studio has multiple parts that can be completed over the course of different class periods. Proceed at your own pace, but be sure to complete them all in order to learn the concepts.

- [Part 1: Persisting a Single Class](single-class-persistence/)
- [Part 2: Setting Up a One-to-Many Relationship](one-to-many/)
- [Part 3: Setting Up a Many-to-Many Relationship](many-to-many/)
