---
author: admintm
categories:
- Go
date: "2016-05-11T15:10:53Z"
guid: http://www.tysonmaly.com/?p=144
id: 144
title: How to use SASS to generate CSS
url: /programming/go/how-to-use-sass/
---

### Using SASS or SCSS to generate CSS with your favorite language

I am not big on using grunt or gulp, but I do like the power of what SASS offers, so I am going to explain a simple method on how you can mix sass with your programming language.   This method will work with any programming language, but I happen to be using this with [Go](http://www.tysonmaly.com/programming/go/learning-golang/) as I work on the re-design of my <a href="https://bestfoodnearme.com" target="_blank" rel="nofollow">food project</a>.

### What is the difference between SASS and SCSS ?

SCSS lets you mix css into your sass and still compile it to css, that is the short and easy answer.

### Why should I use SCSS ?

If you are reading this, you already have an idea, but I will give you my reason.   I like to be able to iterate quickly on my go projects, so I need to be able to change design just as quickly as I change code.  SCSS lets me do this, and it produces very tight css that does not come with all the extra baggage and size of larger frameworks such as bootstrap.

### Install libsass library

The first thing you are going to need is an installed library of libsass.  I chose this library because it is blazing fast compared to the ruby library for SASS.  The dependencies for this C++ library may cause some issues when trying to build it from source.  I ran into issues with dependencies, but you may not want to go this route.   There is an easier method to do this that works on Windows, OSX, and Linux.   I use the Perl module CSS::Sass.  This module handles the building of the C++ library for you automatically when you install it.  If your on Windows, I would recommend you install <a href="http://strawberryperl.com/" target="_blank" rel="nofollow">Strawberry Perl</a>. Most Linux distros come with Perl installed.   If you are on OSX, you should already have Perl, but you may have to install the X Code to get the gcc libraries if you have not already done so.

If you already have Perl installed, fire up the command line and issue this command:

<pre>perl -MCPAN -e shell</pre>

then at the CPAN prompt ( cpan> ) type:

<pre>install CSS::Sass</pre>

After installing this module, you will need to create a small script to use it.

### Using libsass from a script

Here is a short script that I use as part of my process to compile scss to css.  It takes the main scss file as its input and it prints the compiled css to standard out.  If there are any errors it prints those to standard error.  Libsass through CSS::Sass module offers a couple of different ways to output css.  You can output full css that has not been minified with the SASS\_STYLE\_EXPANDED flag.  This will include all the comments and whitespace.  If you want compressed css with comments and whitespace stripped out of your final file, use the SASS\_STYLE\_COMPRESSED flag.

<pre>#!/usr/bin/env perl

use strict;
use CSS::Sass qw(SASS_STYLE_EXPANDED SASS_STYLE_COMPRESSED sass_compile_file);

my $in = $ARGV[0];

my ($css, $err, $stats) = sass_compile_file($in,
output_style =&gt; SASS_STYLE_COMPRESSED);

print "$css\n" if $css;
warn "$err\n" if $err;
</pre>

### Using libsass in a Makefile

I use a Makefile for my Go projects, so I am going to show you a very simple Makefile that calls this script.  You can integrate this into your build process.  In my full Makefile,  I have another step that gzips the css and also generates a Go html/template file that uses a time stamped version of the css.  I also have another step for javascript files to minify them and compress them.   I may add that to this post at a later time, but I wanted to keep things simple for those getting started with SASS.

Here is the Makefile:

<pre>SASS=~/scripts/compile_scss


css:*.scss
$(SASS) ./site.scss &gt; ../css/site.css

</pre>

In this Makefile,  I assume you have a master scss file called site.scss that has of the includes.  I also assume that you have a subdirectory ( in this case called scss ) that contains the Makefile and all of the scss and associated libraries with it.  At the same level as the scss, I assume you have a directory called css.

&nbsp;

### What type of benefits can I get from using SASS or SCSS in my web project?

I am in the process of re-skinning my food site.  The current version uses the bootstrap framework.  This can be quite heavy with all the bells and whistles as well as the themes and javascript, you are looking at around 143 kb.    I recently started using a SASS mixin library called <a href="http://bourbon.io/" target="_blank" rel="nofollow">Bourbon </a> along with a semantic grid called Neat by the same people.  I was able to take my initial design from about 70 kb of compressed files down to 5.9 kb of compressed files.   My load time on my local machine was 63 ms.  So you can achieve some really nice reductions in your files sizes if you use SASS and SCSS.

If your just getting started programming in Go see my post [learning Go](http://www.tysonmaly.com/programming/go/learning-golang/) for some helpful tips.

If you already know Go, here is a great tip to [find Go projects](http://www.tysonmaly.com/programming/go/go-projects/).

### Using libsass with pure Go

media_guru on <a href="https://www.reddit.com/r/golang" target="_blank" rel="nofollow">/r/golang</a> pointed out there is a project called <a href="https://github.com/wellington/wellington" target="_blank" rel="nofollow">wellington</a> that is written in pure Go that wraps the libsass library.  This would be an easier solution for people programming in Go if your on Linux or OSX because there are binaries of libsass provided with the project.  If you do not know how to program in Go, but have an interest, check out my post on [learning golang](http://www.tysonmaly.com/programming/go/learning-golang/).