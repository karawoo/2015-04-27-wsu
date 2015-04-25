---
layout: page
root: ..
title: Introducing Version Control
---

#Teaching Git - 1

1. Take 30 seconds and explain to your neighbor what your project workflow is. What tools do you use? How do you keep notes on what you did?
2. Does your workflow change when you collaborate with other people? How do you communicate?
_3 groups share their answers_

##What is Version Control?
_any guesses?_

__Some questions__

* How easy would it be to grab the code you used to develop a project/manuscript from last week? Last year? Last 5 years?
* How much work would you lose if your laptop was stolen/damaged?
* If you deleted part of your manuscript or analysis, then later realized that you wanted to keep it in, would you have to rewrite it?
* If you were collaborating with someone on a manuscript or some code and someone rewrote something, how easy would it be to track down who changed it and why?

__Version control...__

* keeps track of changes to a file/folder
* keeps a backup of changing files
* stores of history of the changes
* allows you to go back to previous versions of your project
* allows you to work efficiently from multiple computers in multiple locations
* allows many people to make changes concurrently (collaboration!)

__Do you currently use some kind of version control?__

* [The many-folder system](http://hginit.com/i/01-copies.png)
* [Final.doc](http://www.phdcomics.com/comics/archive.php?comicid=1531)
* [cup of USBs](http://www.eeweb.com/rtz/version-control)
* Dropbox
  * only keeps 30-day history
  * longer with "Packrat" but lacks concurrent change ability
* Email files to yourself
* Time Machine (or other automated backup system)

__Suggest that students who are familiar with git and GitHub move to sit near students who are not.
Maybe move to the center of their tables, or towards the aisles to act as helpers??__

##Why should I use a version control system?
__i.e., what makes version control better than Dropbox?__

* keeping lots of copies of files clogs up your system and can be confusing
* sync copies of a project across computers
* easily share project data/code/text with collaborators
* easily pubish/share data/code/text with scientific manuscripts
* __ability to collaboratively code and merge multiple changes__
* __ability to revert to earlier copies when you (or someone else) messes up__

__Scenario 1:__

Wolfman and Dracula have been hired by Universal Missions
(a space services spinoff from Euphoric State University)
to investigate if it is possible to send their next planetary lander to Mars.
They want to be able to work on the plans at the same time,
but they have run into problems doing this in the past.
If they take turns,
each one will spend a lot of time waiting for the other to finish,
but if they work on their own copies and email changes back and forth
things will be lost, overwritten, or duplicated.

The right solution is to use [version control](../../gloss.html#version-control)
to manage their work.
Version control is better than mailing files back and forth because:

*   Nothing that is committed to version control is ever lost.
    This means it can be used like the "undo" feature in an editor,
    and since all old versions of files are saved
    it's always possible to go back in time to see exactly who wrote what on a particular day,
    or what version of a program was used to generate a particular set of results.
*   It keeps a record of who made what changes when,
    so that if people have questions later on,
    they know who to ask.
*   It's hard (but not impossible) to accidentally overlook or overwrite someone's changes:
    the version control system automatically notifies users
    whenever there's a conflict between one person's work and another's.

> ### Challenge {.challenge}
>
> On Wikipedia all changes and their authors are tracked. You can go
> [here](https://en.wikipedia.org/w/index.php?title=Mars&action=history)
> and you will find the history of all changes done to the article about the planet
> Mars. Find the last edit done last month and look at the changes made by
> clicking on the "prev" link on the left of the history entry.

This lesson shows how to use
a popular open source version control system called Git.
It is more complex than some alternatives,
but it is widely used,
both because it's easy to set up
and because of a hosting site called [GitHub](http://github.com).
No matter which version control system you use,
the most important thing to learn is not the details of their more obscure commands,
but the workflow that they encourage.
