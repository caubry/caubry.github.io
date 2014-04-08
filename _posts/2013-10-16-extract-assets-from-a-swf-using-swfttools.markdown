---
layout: post
title: Extract assets from a SWF - Using swfttools
date: 2013-10-16 16:08:21.000000000 +01:00
tags:
- Command Line Tools
---
Today, I was wondering if it was possible to extract assets from a SWF file.  
The answer is YES it is! And it isn't too hard either.

* **Download swftools**

Firstly, **get/download a SWF** file from your machine/the internet : ]  
Then, you can either download the **swfttools** as an EXE or as a TAR at: [http://www.swftools.org/download.html](http://www.swftools.org/download.html)  
If you are a __Github__ lover, simply grab the repo, such as: 

    git clone git://git.swftools.org/swftools

In order to extract assets from a SWF file, you can use the **SWFExtract program** provided with **swftools**.  
If you wish to see more information on different programs that swftools offers, visit this page: [http://www.swftools.org/about.html](http://www.swftools.org/about.html).

* **Install swftools**

There are two ways to install swftools, by the source code (recommended for Unix/Linux/BSD) or by running a binary file (recommended for Windows).  
Further information can be found at: [http://wiki.swftools.org/wiki/Installation](http://wiki.swftools.org/wiki/Installation).  
Once the installation is over, you should be able to run, in your command line 'man swfextract' and get the manual for this specific program.  
If you can't achieve this, please refer back to the installation guide, as you might have missed a trick or two:

**Let the fun begin!**

I've downloaded a panda.swf and I've saved it on my Desktop.  
If I wish to see what is inside this file, I can simply run this command from my Desktop directory:

    swfextract panda.swf

Now, I'm getting something like:

    Objects in file panda.swf:
      [-i] 36 Shapes: ID(s) 28, 30, 33, 36, 38, 40, 42, 44, 46, 48, 50, 52, 54, 56, 58, 60, 62, 64, 66, 68, 70, 72, 74, 76, 78, 80, 82, 84, 87, 91, 119, 120, 123, 129, 130, 143
      [-i] 9 MovieClips: ID(s) 31, 34, 35, 135, 136, 144, 147, 175, 191
      [-j] 2 JPEGs: ID(s) 27, 86
      [-p] 2 PNGs: ID(s) 29, 32
      [-s] 26 Sounds: ID(s) 2-26, 92
      [-F] 4 Fonts: ID(s) 88, 126, 149, 181
      [-M] 8 Embedded MP3s: ID(s) 31, 34, 35, 136, 144, 147, 175, 191
      [-f] 1 Frame: ID(s) 0
      [-m] 1 MP3 Soundstream

You might also get something with Binarys, like:

    Objects in file panda.swf:
      [-i] 1 Shape: ID(s) 1
      [-b] 2 Binarys: ID(s) 2, 3
      [-f] 1 Frame: ID(s) 0

Note that Binarys can hold a second SWF file =o  
To output a binary into a custon file name, such as myBinaryFile, simply run:

    swfextract -b 2 panda.swf -o myBinaryFile

details:

    swfextract -b [ID] [input file] -o [output file]

Note that I didn't give an extension name to the output, so you can test if it is a Flash file, by simply open it.  
You should get a Flash error... if you do, you know it's a Flash file : D  
If you don't, you might want to try a different Binarys ID.

If it is a Flash file, you can output it the same way as earlier, using swfextract:

    swfextract myBinaryFile

In this example, taken from panda.swf, I want to extract the sounds from 2 to 26 and the 92 one.

    [-s] 26 Sounds: ID(s) 2-26, 92

Sounds will be placed into a folder named 'sounds', in the current directory:

    # !/bin/bash
    for NUM in {2..26} 92
    do
        swfextract -s $NUM panda.swf -o "sounds/sound_$NUM.mp3"
    done
