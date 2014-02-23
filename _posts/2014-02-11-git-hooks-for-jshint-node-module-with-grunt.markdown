---
layout: post
title: Git hooks for jshint node module with Grunt
date: 2014-02-11 22:34:44.000000000 +00:00
tags:
- grunt
- jshint
- githooks
- node
- Deployment
---

**Install Grunt Git hooks** (Assuming that jshint is already running)

This hook will be run before each commit.  
Create a package.json to be executed when running:
    npm install

Or simply install grunt-githooks in the project:
    npm install grunt-githooks --save-dev

Create/update the Gruntfile.js file  
Example:

```
    module.exports = function(grunt) {
        grunt.initConfig({
            jshint: {
              files: ['js/*'],
              options: {
                // options here to override JSHint defaults
                globals: {
                  jQuery: true,
                  console: true,
                  module: true,
                  document: true
                }
              }
            },
            githooks: {
              all: {
                'pre-commit': 'jshint'
              }
            }
        });

        // Load tasks
        grunt.loadNpmTasks('grunt-contrib-jshint');
        grunt.loadNpmTasks('grunt-githooks');

        // Register tasks
        grunt.registerTask('default', ['githooks', 'jshint']);
    }
```

Run Grunt Git Hooks as a test:

    grunt githooks

![Grunt Githooks Command Screenshot](/images/githooks.png "Grunt Githooks Command Screenshot")

Whenever you want to commit any install packages added as a 'pre-commit' will run.  
Here running jshint module and abort the commit due to jshint warnings:

![Warning Pre commit Command Screenshot](/images/warnings-commit.png "Warning Pre commit Command Screenshot")

Once corrections have been made, you can stage them again (git add -A) and commit your files:

![Valid Pre commit Command Screenshot](/images/valid-precommit.png "Valid Pre commit Command Screenshot")

