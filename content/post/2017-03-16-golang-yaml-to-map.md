---
author: admintm
categories:
- Go
date: "2017-03-16T02:27:59Z"
guid: http://www.tysonmaly.com/?p=208
id: 208
title: Golang YAML to map
url: /programming/go/golang-yaml-to-map/
---

## How to convert a YAML file to a map[string]string in Go

Use <a href="https://github.com/tvmaly/go-yamlconfigfile" target="_blank" rel="nofollow">go-yamlconfigfile</a> project to convert simple yaml config files to maps in Go.

When you want to store secrets for your project, you should never keep them in source control.  There have been too many documented cases of secrets being leaked because of this.  If you are using public version control like github, people can simple scan through your history to find things you may have accidentally released to the public internet.

I am using just a simple YAML file with a single level to hold my API keys.  You should have a .gitignore file and you should add

*.yaml to this file.

Before your check in your code to github or other version control, double check that your YAML file is not included.

In git I use the command

<pre>git status -v</pre>

If you do not see your file on the list, you are safe.

My simple utility package exports a single function  LoadYAMLFile

This function takes a path to a YAML file, and it returns a map[string]string and an error

Example:

yaml, err := LoadYAMLFile(&#8220;test.yaml&#8221;)

This could easily be expanded to multiple levels in the YAML file, but I wanted to keep things simple.

If you have any questions or issues with the project, ping me on github/tvmaly

&nbsp;