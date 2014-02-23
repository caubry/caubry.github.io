---
layout: post
title: JavaScript animation using requestAnimationFrame and set a FPS
date: 2014-02-14 16:11:51.000000000 +00:00
tags:
- JavaScript
- html5
- requestAnimationFrame
---

Commonly, creating animations in JavaScript requires the use of __setTimeout__ and/or __setInterval__.
Unfortunately, relying on these methods only can cause issues to the users, as elucidated to on the [CreativeJS site](http://creativejs.com/resources/requestanimationframe/). When using __setTimeout__, the browser doesn't take into consideration if the page has been hidden behind a tab and can cause some CPU and/or animation issues. This method also doesn't take into account computer performance and will contently try to update the page, disregarding CPU usage.  
Clearly not good for the lifetime of any device...  
Modern browsers such as Mozilla, Chrome and Safari offer an alternative to the methods above, with a __requestAnimationFrame__ function. It provides a native API for running any type of animation in the browser.  
Unfortunately, as it's an API, it's only currently available in browsers via a vendor prefix.  
Luckily, Eric M&ouml;ller, Paul Irish and Tino Zijdel have created a [polyfill](http://remysharp.com/2010/10/08/what-is-a-polyfill/) to get around this issue:  
[(Gist)](https://gist.github.com/paulirish/1579671)
```
    // http://paulirish.com/2011/requestanimationframe-for-smart-animating/
    // http://my.opera.com/emoller/blog/2011/12/20/requestanimationframe-for-smart-er-animating 
    // requestAnimationFrame polyfill by Erik M&ouml;ller. fixes from Paul Irish and Tino Zijdel
    // MIT license
     
    (function() {
        var lastTime = 0;
        var vendors = ['ms', 'moz', 'webkit', 'o'];
        for(var x = 0; x < vendors.length && !window.requestAnimationFrame; ++x) {
            window.requestAnimationFrame = window[vendors[x]+'RequestAnimationFrame'];
            window.cancelAnimationFrame = window[vendors[x]+'CancelAnimationFrame'] 
                                       || window[vendors[x]+'CancelRequestAnimationFrame'];
        }
     
        if (!window.requestAnimationFrame)
            window.requestAnimationFrame = function(callback, element) {
                var currTime = new Date().getTime();
                var timeToCall = Math.max(0, 16 - (currTime - lastTime));
                var id = window.setTimeout(function() { callback(currTime + timeToCall); }, 
                  timeToCall);
                lastTime = currTime + timeToCall;
                return id;
            };
     
        if (!window.cancelAnimationFrame)
            window.cancelAnimationFrame = function(id) {
                clearTimeout(id);
            };
    }());
```

You can just use this polyfill like so:

```
    requestId: 0,
    move: function() {
      var _this = this;
     
      if (this.requestId === 0) {
        (function animationLoop() {
          _this.render();
          _this.requestId = requestAnimationFrame(animationLoop, _this.move);
        })();
      }
    },
     
    render: function() {
      // Add some drawing
    },
     
    onKeyUp: function() {
      // Cancel the animation request
      if (this.requestId) {
        cancelAnimationFrame(this.requestId);
      }
      // Allow a new request to be called
      this.requestId = 0;
    }
```

That works fine!  
Unfortunately, this doesn't take into account the FPS (frame per seconds) of your game. A work around is to use the method __setTimeout__ in conjunction with the polyfill, such as:

```
    requestId: 0,
    settimeoutID: 0,
     
    move: function(keyCode) {
      var _this = this;
      // Frame per seconds
      var fps = 15;
      
      if (this.requestId === 0) {
        (function animationLoop() {
          // Control the timing of an animation with requestAnimationFrame
          _this.settimeoutID = setTimeout(function() {
            _this.render();
            _this.requestId = requestAnimationFrame(animationLoop, _this.move);
          }, 1000 / fps);
        })();
      }
    },
     
    render: function() {
      // Add some drawing
    },
     
    onKeyUp: function() {
      // Cancel the animation request
      if (this.requestId) {
        clearTimeout(this.settimeoutID);
        cancelAnimationFrame(this.requestId);
      }
      // Allow a new request to be called
      this.requestId = 0;
    }
```

Of course, using this method allows anyone to easily change the FPS and most importantly, controls the timing of an animation across multiple browsers. 
