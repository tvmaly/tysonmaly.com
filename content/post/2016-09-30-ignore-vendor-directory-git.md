---
author: admintm
categories:
- Go
date: "2016-09-30T11:06:03Z"
guid: http://www.tysonmaly.com/?p=197
id: 197
title: How to ignore vendor directory in git for Go projects
url: /programming/go/ignore-vendor-directory-git/
---

You accidentally added your vendor directory to git in your Go project.   Now when you run git status you see all these modified files under the vendor directory.

Here is a quick command you can use to ignore these changes

First change to your project directory then run this command

git status | perl -ne &#8216;/(vendor.+go)/ && system &#8220;git update-index &#8211;assume-unchanged $1\n&#8221;;&#8217;

This will take each file mentioned in the status that is in your vendor directory and execute a git command against it to

tell git to stop tracking it.

In the long run, you should probably not add your vendor directory to your VCS.  For git, you should create a .gitignore file under your project directory and add vendor/ in that file.

Here is a complete .gitignore file that you can use for your Go projects from <a href="https://github.com/github/gitignore" target="_blank" rel="nofollow">here</a>:
  
*.o
  
*.a
  
*.so

\# Folders
  
_obj
  
_test

\# Architecture specific extensions/prefixes
  
*.[568vq]
  
[568vq].out

*.cgo1.go
  
*.cgo2.c
  
\_cgo\_defun.c
  
\_cgo\_gotypes.go
  
\_cgo\_export.*

_testmain.go

*.exe
  
*.test
  
*.prof

\# Output of the go coverage tool, specifically when used with LiteIDE
  
*.out

\# external packages folder
  
vendor/

&nbsp;