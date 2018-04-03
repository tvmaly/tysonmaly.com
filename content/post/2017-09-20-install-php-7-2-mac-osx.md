---
author: admintm
categories:
- osx
date: "2017-09-20T13:22:33Z"
guid: http://www.tysonmaly.com/?p=226
id: 226
title: How to install PHP 7.2 on Mac OSX
url: /mac-os/install-php-7-2-mac-osx/
---

# How install the latest stable version of PHP 7.2 on OSX using homebrew.

As of this writing PHP 7.2 is still not the official production release, but you can still install it on OSX.

The motivation for writing this post was because I wanted to upgrade from the PHP 5.6 on my mac book to the latest stable version for WordPress development on OSX.  WordPress is phasing out support for older versions of PHP.

This assumes you are using homebrew and know how to use the commandline using either the build in terminal or the iTerm2.

Open a terminal window then
  
check which version of php you have with the command

<pre>php -v</pre>

we want to use at least version 7

Next update your brew and upgrade existing packages

<pre>brew update && brew upgrade</pre>

if you get some errors for some packages you are not using, what can you do?

Remove them of course.  How do you remove homebrew packages?

Use the rmtree to remove homebrew packages.  Here is how you can install and use rmtree:

<pre>  brew tap befftornado/rmtree
  brew rmtree &lt;package&gt;
</pre>

Next follow these steps to install php 7

<pre>brew tap homebrew/php
brew unlink php56
brew install php72

If you get an error message running the unlink, it just means you did not install that version with homebrew.</pre>

Finally run one more check on the commandline to see the version

<pre>php -v

If you get any errors about shallow copy you can run this command

git -C "$(brew --repo homebrew/core)" fetch --unshallow</pre>