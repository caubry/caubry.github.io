---
layout: post
title: "Jasmine and CoffeeScript"
date: 2014-05-05 11:53:39.000000000 +01:00
tags:
- Jasmine
- CoffeeScript
---

Last week at work, I was asked to work on a mobile game, using pretty much what I fancy in conjunction with [createJs](http://www.createjs.com/). While we mainly make use of CoffeeScript, which is a language that compiles to JavaScript, I thought I should give it a go in order to keep everything consistant :)    

While thinking of a good way to start working on my new project, I've realised that as I'm going to use a new language, I should aim to ensure that no mistakes are made, or at least, any errors are spotted ASAP :D. This is why, I've decided to go for a __Test Driven Development__ (TDD) project. 

As it's the first time I've used TDD, I made some preliminary research and came across [Jasmine](http://jasmine.github.io/), a popular Behaviour Driven Development (BDD) framework.    

I've followed the [CoffeeScript Cookbook](http://coffeescriptcookbook.com/chapters/testing/testing_with_jasmine) guide to setup Jasmine, and this guide about [organizing a CoffeeScript project](http://k20e.com/blog/2011/05/02/a-piece-of-cakefile/) to help me getting started with my game development project with CoffeeScript and Jasmine. The latter also helped me to create my first Cakefile. As the [CoffeeScript documentation](http://coffeescript.org/documentation/docs/cake.html) cites, *cake is a simplified version of Make (Rake, Jake) for CoffeeScript. You define tasks with names and descriptions in a Cakefile, and can call them from the command line, or invoke them from other tasks.* It's a really handy package when you want to quickly compile a project, minify a file etc.    

### Cakefile ###

In the project I've setup, which is located on [Github - jasmine-and-coffeescript-template](https://github.com/caubry/jasmine-and-coffeescript-template), I've used 7 cake tasks inside ./Cakefile:    

* **watch:all**: To watch production and test CoffeeScript. If you are unfamiliar with the term *watch*, it basically listens out for changes in the file you are currently working on and gives you the ability to see these changes instantly instead of manually building yourself;
* **build:all**: To build production and test CoffeeScript. Therefore, this allows me to open my ./SpecRunner.html, which is the Jasmine test page and see any fails in my program, but also to run my /public/index.hmtl page and play my current game. This task also calls the *uglify* task, cited below;
* **watch**: To watch production source files and build changes only;
* **build**: To compile production CoffeeScript into JavaScript and build a single JavaScript file using *uglify* task;
* **watch:test**: To watch test specs and build changes;
* **build:test**: To compile CoffeeScript files into JavaScript individual test specs;
* **uglify**: To minify my production files into a single obfuscated JavaScript file located in /public/js/app.min.js

In order to use these tasks while working on my project, I'm using a Sublime Text 2/3 plugin named [Better CoffeeScript](https://sublime.wbond.net/packages/Better%20CoffeeScript). This package comes in very handy for syntax highlighting, shortcuts, snippets and watched compilation. I mainly use it to run my custom Cake tasks straight from Sublime.    

### Structure project ###

Regarding the way my project is setup:

* **/app**: This is a folder that contains my production files;
* **/public**: This is folder for any files that are served by the web server;
* **/spec**: This is a folder for my test files only, where Jasmine lives;
* **./Cakefile**: As cited above, this file groups all my Cake tasks;
* **./SpecRunner.html**: This page allows me to display test output within a browser.

Finally, as I am still in the process of learning Jasmine, I often look at the [Jasmine introduction](http://jasmine.github.io/2.0/introduction.html) page to understand the Jasmine syntax. So far I have to admit that it's a bit tedious, but I'm pretty convinced that I will quickly see the benefits of TDD.    

###Jasmine CoffeeScript Template###

If you wish to install my Jasmine CoffeeScript Template located at [Github - jasmine-and-coffeescript-template](https://github.com/caubry/jasmine-and-coffeescript-template), you can follow the procedure below. Of course, if anyone has any improvements, I would love to hear about them :)    

Run *./package.json* in the current project directory to install node modules dependencies:    

    npm install

Add the node modules folder to your $PATH, if you haven't done it yet. If you are unsure where the folder is located simply run:    

    which cake

*Note: On Windows, node modules are usually located at: C:\Users[name]\AppData\Roaming\npm. On OSX, you can often find them at: /usr/local/bin*

Once added, you can run:    

    cake build:all

You should get your CoffeeScript files compiled into JavaScript and minified using the node module uglify.    
Launch the *./SpecRunner.html* using your web browser - every test should pass :)

![Jasmine Test Pass](/images/jasmine_tests_pass.png "Jasmine Test Pass")

### Writing test commands ###
You can now start writing your CoffeeScript commands tests in /spec/src/coffee-script    
If you wish to listen out for changes in the file you are currently working on, you can run:     

    cake watch:test

When this is done, you can compile them to JavaScript, by running the command:

    cake build:test

When the build is done, you should be able to notice some changes in /spec/src/js    
To ensure, your commands are syntaxly correct, simply launch the *./SpecRunner.html* into a web browser once again. At this point, your new test commands should failed.    

![Jasmine Test Fail](/images/jasmine_tests_fail.png "Jasmine Test Fail")

This is great, you now need to write the code that will make your commands pass every test.     

### Writing production commands ###
The production code for CoffeeScript is located at /app/src/coffee-script    
If you wish to listen out for changes in the file you are currently working on, you can run:   

    cake watch

Once you are happy with your CoffeeScript, you can run the following command: 

    cake build

You should be able to notice changes in /app/src/js, as well as /public/js/app.min.js    
The command you just ran, compiled all of your CoffeeScript located in /app/src/coffee-script into a JavaScript file located at /app/src/js/app.js    
It also minifies every JavaScript files (in case you need to include some JavaScript files within this folder) located at /app/src/js into a single JavaScript file located at /public/js/app.min.js    

You can now launch */public/index.html* into a web page and see your current project working on this page. If you followed the previous step and wrote some test commands, you should now be able to pass your tests. Check this out by launching *./SpecRunner.html*.    
If not, just follow the TDD procedure and just try again :p