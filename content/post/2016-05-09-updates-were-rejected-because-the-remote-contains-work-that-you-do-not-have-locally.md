---
author: admintm
categories:
- Git Version Control
date: "2016-05-09T14:59:16Z"
guid: http://www.tysonmaly.com/?p=141
id: 141
title: Updates were rejected because the remote contains work that you do not have
  locally
url: /programming/git/updates-were-rejected-because-the-remote-contains-work-that-you-do-not-have-locally/
---

Updates were rejected because the remote contains work that you do not have locally.  That is the error message you may get from git when you try to push your changes to the remote repository.

Here is how to solve the problem of trying to commit to a git repository after you made changes but then someone else already committed ahead of you.  Another way to look at this is that you forgot to perform a

<pre>git pull</pre>

before you started coding in order to get the most recent version of the code.

If you try to commit your local changes to the remote branch, you will get the error message in the title of this post.  If you want see what is going on, run the following command to display where you are and where the head of the branch you are on is:

git branch -va

This command will show you all the remote and local branches.

So here is how we are going to solve this problem.  Run the following command to get the most recent changes from the remote branch and then apply your new changes on top of those changes.

git pull &#8211;rebase