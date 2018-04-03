---
author: admintm
categories:
- Go
- osx
date: "2016-09-30T11:23:32Z"
guid: http://www.tysonmaly.com/?p=199
id: 199
title: How to compile libvips on OSX from source for image processing
url: /programming/go/compile-libvips-osx-image-processing/
---

Here are the steps needed to compile libvips from source.  If you try to install it from homebrew, you will most likely run into a number of errors regarding the dependency  gtk-doc.  This will frustrate you, and you might abandon the effort.  I will show you how to install the latest stable libvips without having to install gtk-doc

I normally do not like to use dependencies like this in my Go project, but the performance of image processing needs to be really good as this type of computing tends to use a ton of resources on a server.

There are a number of homebrew installs you can use to speed this process up.  Before we get started, make sure you have XCode installed along  with the command line tools.  Also make sure you have homebrew installed.  Then follow these steps to build libvips on osx.

0.  brew install autoconf automake libtool

First install libxml2

  1. brew install libxml2

Next run this command as root to link  the installed libxml2

2. sudo brew link libxml2

check that /usr/local/lib/ has entries for libxml2 pointing to your homebrew area  also check that

/usr/local/include/libxml2 points  to your homebrew install of libxml2

Now install the nasm

3. brew install nasm

Now you want to download and compile libjpeg-turbo

4. git clone https://github.com/libjpeg-turbo/libjpeg-turbo

5. cd into that folder and run the following commands:

autoreconf -fiv
  
./configure
  
make
  
sudo make install

check that the install places the files under /opt/libjpeg-turbo/

&nbsp;

6.  cd to your general git folder where you keep all cloned source and clone libvips source

git clone https://github.com/jcupitt/libvips

7.  assuming that libxml2 in step 2 is in expected area and libjpeg-turbo in step 5 is in expected area cd into the cloned source of libvips and run the following commands

./configure &#8211;with-jpeg-libraries=/opt/libjpeg-turbo/lib &#8211;with-jpeg-includes=/opt/libjpeg-turbo/include CFLAGS=&#8221;-I/usr/local/include/libxml2&#8243; LDFLAGS=&#8221;-L/usr/local/lib&#8221;

make

sudo make install

8. Finally check everything was installed by going to /usr/local/lib  if you see the libvips with recent timestamps you have installed from source libvips on osx
