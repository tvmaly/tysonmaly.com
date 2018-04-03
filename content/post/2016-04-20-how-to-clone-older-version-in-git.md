---
author: admintm
categories:
- Git Version Control
date: "2016-04-20T16:19:59Z"
guid: http://www.tysonmaly.com/?p=23
id: 23
title: How to clone old version in git
url: /programming/git/how-to-clone-older-version-in-git/
---

## Here is how you clone an old version in git

You can also use this method to clone a specific commit in a git project.

In this example I needed to get a previous version of one library in git that is a dependency for another supporting library.

Often what happens is new development is taking place, and one library may have commits that are not compatible with another library.

I just started using bourbon sass library, and it is undergoing a major version change.  I wanted to use the current stable version 4 and the other supporting library called bitters.  The author of bourbon said that I needed to use bitters version 1.2

First thing I do is go to the project on github and click on the commits to see which commit value is used on version 1.2 in this case.  Scroll down till you see mention of version 1.2 the commit hash in this example is 95cd30a

The first thing you need for this example to do is open up a terminal to the command line and run the following command:

    git clone https://github.com/thoughtbot/bitters 

This creates a sub-directory called bitters in my current directory. Now change into the cloned project sub-directory with the command:

    cd bitters

&nbsp;

and run the following command to get the specific SHA-1 hash commit:

    git checkout 95cd30a
    

Finally, you can use the following command to check that you successfully cloned the old version from github with the following command:

    git log

The first commit at the top of the screen should start with 95cd30a your SHA-1 hash