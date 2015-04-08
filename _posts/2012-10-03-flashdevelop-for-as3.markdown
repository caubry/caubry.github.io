---
layout: post
title: Setting up FlashDevelop for AS3
date: 2012-10-03 19:01:39.000000000 +01:00
tags:
- FlashDevelop
---

I was recently refreshing my memory over how to set up FlashDevelop, but was unable to find any sufficient resources on the Web.
So here it is: after installing FlashDevlop, open Adobe Flash.
Create a new Document: File > New... > ActionScript 3.0 and on the properties tab, add a name to your class, commonly named "Main":

<img class="img-thumbnail" src="/images/nameclass.png" alt="ActionScript 3.0 Class" title="ActionScript 3.0 Class"/>

**Save your Adobe Flash file into an empty folder.**
Launch FlashDevelop.exe and create a new project:  
Project > New Project... > Under ActionScript 3, select Flash IDE Project:

<img class="img-medium" src="/images/newproject.png" alt="FlashDevelop - Create new projet" title="FlashDevelop - Create new projet"/>

Give a name to your new project and choose the **same location as your Adobe Flash project.**  
Make sure "create directory for project" is un-ticked:

<img class="img-medium" src="/images/namefd.png" alt="FlashDevelop - Create a directory" title="FlashDevelop - Create a directory"/>

When clicking OK, a warning popup will appear. Do not worry, this is only because you have a Flash file already in this folder.
Click OK.

<img class="img-medium" src="/images/warning.png" alt="FlashDevelop - Warning" title="FlashDevelop - Warning"/>

If FlashDevelop requests it, choose an author name.  
Create a New Class by right clicking through the main project folder in the right sidebar: Add > New Class...

<img class="img-small" src="/images/newclass.png" alt="FlashDevelop - New Class" title="FlashDevelop - New Class"/>

Give the same Class name as the one you've previously created on Adobe Flash.  
Extend the MovieClip class, and FlashDevelop will automatically add the line to import the library MovieClip library.  
Run a trace like so:

<img class="img-small" src="/images/mainclass.png" alt="FlashDevelop - Main Class" title="FlashDevelop - Main Class"/>

At this point, your script won't run, as you need a MovieClip, so go ahead and create one (Insert > New Symbol...).  
Give your MovieClip a name and make sure to tick "Export for ActionScript".
Click OK.

<img class="img-small" src="/images/newsymbol.png" alt="FlashDevelop - New Symbol" title="FlashDevelop - New Symbol"/>

Draw something and save it.

<img class="img-thumbnail" src="/images/randomsymbol.png" alt="FlashDevelop - Random Symbol" title="FlashDevelop - Random Symbol"/>

You should now be able to run your script from FlashDevelop and/or Adobe Flash by pressing Ctrl + Enter.