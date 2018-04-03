---
author: admintm
categories:
- Go
date: "2016-09-15T14:46:31Z"
guid: http://www.tysonmaly.com/?p=194
id: 194
title: Golang Vendoring How to add vendoring to an existing Go project
url: /programming/go/golang-vendoring-how-to-add-vendoring-to-an-existing-go-project/
---

# How to add Vendoring to an existing Go Project to manage your dependencies

In this post I want to discuss how you can add vendoring for your dependencies to an existing Go project that does not currently have a vendor directory.

I am working on a new version of <a href="https://bestfoodnearme.com" target="_blank" rel="nofollow">Best Food Near Me</a>.  The original version used a version of Go that did not have vendoring support, but it has since been upgraded.  Some of my dependencies had changed, and things did not work the same.  I decided it would be prudent to add vendoring to my new version to better track changes in my dependencies.

There are a number of tools that can help make use of the vendor feature easier.  I tried a number of them such as <a href="https://github.com/tools/godep" target="_blank" rel="nofollow">GoDep</a> and <a href="https://github.com/kardianos/govendor" target="_blank" rel="nofollow">GoVendor</a> but they did not work as well against an existing project.  If you are starting a new project from scratch, I am sure they would be a better fit.

I settled on using Glide as the tool to help me manage the dependencies in my vendor directory of my Go project.  Here are the steps I took

  1. Install Glide 
        curl https://glide.sh/get | sh

  2. Inside you project directory make a vendor directory
  3. copy one dependency into the vendor directory from GOPATH
  4. run &#8220;glide create&#8221;  inside  your project directory and choose semantic versioning and Minor patches when it prompts you.
  5. You should now have a glide yaml file at this point.  Now for each dependency not in your vendor subdirectory  run    glide get github.com/foo/bar   for each replacing foo and bar with the actual paths for that dependency

There is a chance that some of your dependencies do not have a git tag for a semantic version, that is ok,  if there is a specific git commit hash you would like to pin to, you can edit the yaml file and add a version for a dependency and specify the full hash commit.

You can check which dependencies you have currently vendored with the list command

<pre>glide list</pre>

If you want to update all of your dependencies in the vendor directory you can use the command

<pre>glide up</pre>

I hope you have found this short post useful information.  If you have, please share.