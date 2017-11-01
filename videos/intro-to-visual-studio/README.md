---
title: Intro to Visual Studio
currentMenu: videos
---

<div class="youtube-wrapper"><iframe width="776" height="437" src="https://www.youtube-nocookie.com/embed/t5F4-7DYAhY?rel=0" frameborder="0" allowfullscreen></iframe></div>

## Notes

To publish a new Visual Studio project to GitHub:
* Open the Team Explorer tab (and click on the Home icon if you do not see the option below)
* Select "Sync"
* Select the "Publish to GitHub" option and select your username from the dropdown. Then click "Publish"

To commit and push changes:
* In the Team Explorer tab, on the Home screen, select "Changes"
* Add a commit message in the box
* Choose from the dropdown to either "Commit All" your changes locally, or to "Commit All and Push" your changes to the remote

To clone a repo from GitHub to your computer locally:
* In the Team Explorer tab, click on the *Manage Connections* icon (see below)
* Select *Clone* from the GitHub section and select your repository from the modal window
* Change the Path field to the location at which you would like the project to live, ideally inside of a folder - like `lc101` - that you've been using to store other projects
* Then click "Clone"

	![Manage Connections](../images/team-explorer-connections.png)
	
If you haven't already done so by following the initial setup instructions exactly from Class 1, set the project startup configuration below.

Right-click on the top-level "Solution" item in the *Solution Explorer* and select *Properties*. (If right-clicking doesn't work, just select "Solution" and then click the tool/wrench icon near the top of *Solution Explorer*). In the modal that opens, select *Common Properties > Startup Project* and then choose *Current Selection* in the pane at the right.

## References

- [Visual Studio IDE (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/dn762121.aspx)
