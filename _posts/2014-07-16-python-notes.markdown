---
layout: post
title: "Creating a desktop application using Python - wxPython"
date: 2014-07-16 21:00:39.000000000 +01:00
tags:
- Python
- Pubsub
---
This post aims to group the GUI Programming and Design tools that I found the most interesting while creating a desktop application in Python. 

### GUI toolkit ###
Python has a wide range of GUI frameworks, also called toolkits, available for those wishing to create applications. 
I've chosen *wxPython* over *Tkinter* simply because *wxPython* offers more advanced widgets as well as using native operating system ones. The only downside is that this toolkit isn't part of the standard Python distribution and so has to be downloaded and installed separately.
This isn't too much of a downside if you want to package the application into an EXE for the end-user, once your project is finished.    
You can download the most up to date version of *wxPython* at: [http://www.wxpython.org/download.php](http://www.wxpython.org/download.php).
Here is an example of using wxPython to create a *Hello World* module:

```
#!/usr/bin/env python
import wx
 
app = wx.App(False)  # Create a new app, don't redirect stdout/stderr to a window.
frame = wx.Frame(None, wx.ID_ANY, "Hello World") # A Frame is a top-level window.
frame.Show(True)     # Show the frame.
app.MainLoop()
```

### Python Packages ###
As well as using a great python wrapper, I wanted to make sure that my code would be scalable, clear and tidy. I came accross *PyPubSub*, which is a package that enables a publish-subscribe Python API in order to create an event-based programme. Coming from JavaScript and ActionScript I found this design pattern very useful. I've used this package alongside the Model-View-Controller pattern.    
You can download *PyPubSub* package at: [http://sourceforge.net/projects/pubsub/files/pubsub](http://sourceforge.net/projects/pubsub/files/pubsub).

### GUI designer ###
When writing my Python application I found it difficult to create a nice front-end design without having to read the *wxPython* documention and look for the right widget.
After doing some research I found that not only I could use a GUI designer to create my front-end design, but I could also easily export the *wxPython* code into my application and make some changes to the code whenever I want.
There are a few tools out there, but I chose to use *wxGlade*, as it seemed the most suitable.    
Can be downloaded at: [http://wxglade.sourceforge.net](http://wxglade.sourceforge.net).    
For more information on GUI Programming in Python you can visit this [page](https://wiki.python.org/moin/GuiProgramming).
