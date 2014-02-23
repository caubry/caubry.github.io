---
layout: post
title: Setting up an AS2 project using MTASC
date: 2013-02-01 13:50:08.000000000 +00:00
tags:
- MTASC
---
It's sometimes easy to forget the different steps in setting up your development environment as it doesn't often need doing. Here are the simple steps I took when setting up MTASC for AS2.

####Main.as####

The static method 'main' in Main.as will be used to run MTASC.  
This is important to include it, as MTASC will make use of it as a single point of entry.  
See "- main" MTASC option in [run.sh](#a0).

```
    import MouseTrail.Interface;
     
    class MouseTrail.Main 
    {
        private static var m:Main;
        var int:Interface;
     
        public function Main(root:MovieClip)
        {
            int = new Interface(root);
        }
     
        public static function main(root:MovieClip)
        {
            m = new Main(root);
        }
    }
```

####Interface.as####

You can now use any Classes you want from your library, because of the "-cp" MTASC option.

```
class MouseTrail.Interface
{
    private var pen:MovieClip;
 
    public function Interface (root:MovieClip)
    {
        var c:MovieClip= root.createEmptyMovieClip("test", root.getNextHighestDepth());
        
        // Do something
    }
}
```

<a name="a0">run.sh</a>


This script contains the MTASC command line, with four options:

- "-swf" refers to your input.
- "-main" refers to your static method (see above).
- "-out" refers to your output.
- "-cp" refers to your classes root folder.

```
# !/bin/bash
ROOT= ~/Desktop/TODO
mtasc $ROOT/mousetrail/src/MouseTrail/Main.as -main 
-swf $ROOT/mousetrail/bin/mouseTrail.swf 
-out $ROOT/mousetrail/bin/Interface.swf 
-cp $ROOT/mousetrail/src
open $ROOT/mousetrail/bin/Interface.swf
```
