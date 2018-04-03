---
author: admintm
categories:
- Programming
tags:
- Go
- golang
date: "2016-04-21T16:49:15Z"
guid: http://www.tysonmaly.com/?p=58
id: 58
images: [/images/go-projects.png]
title: Go projects
url: /programming/go/go-projects/
---

## Go Projects

Here is a very useful tip for finding go projects based on a keyword search.   I recently had to parse a large number of Excel xlsx and xls files for a regulatory compliance request.  I would have traditionally used a Perl module for this, but the version of the module for xlsx that I had was prone to some memory issues.  Go does not really have a <a href="http://www.cpan.org/" target="_blank" rel="nofollow">CPAN</a> for those just [learning golang](http://www.tysonmaly.com/programming/go/learning-golang/).

I was curious how much faster Go could perform against Perl, so I ran a benchmark on a regular data parsing task that I perform.  I found that Go performed 5 times to 10 times faster than Perl for this task.

So I decided for this Excel parsing task, I would create a Go project to parse the Excel files.

Before I re-invent the wheel,  I always perform a search to see if someone has already written something that does what I want or close to it.   Go projects are numerous and abundant, and growth has been off the charts.  Before I found this Go trick, I would have to scavenge the golang-nuts Google group or the sub reddit /r/golang .  It was already a habit just to see what people were releasing, but still this technique works a lot faster for finding Go projects.

The golanglibs.com website indexes all of the golang projects that are publicly available on the internets.

So to search for any publicly available Go project that has the keyword xlsx in it use the following query

<a href="https://golanglibs.com/search?q=xlsx" target="_blank" rel="nofollow">https://golanglibs.com/search?q=xlsx</a>

Now going forward, it you want to search for a Go project that has a keyword, simply replace the xlsx in the query with your keyword.

I hope this method helps you in your journey to improve your Go skills.  Its early here so I need to make some [strong coffee](http://www.tysonmaly.com/recipes/how-to-make-strong-coffee/).  Till next time..
