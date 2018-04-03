---
author: admintm
categories:
- Git Version Control
date: "2016-04-21T15:56:50Z"
guid: http://www.tysonmaly.com/?p=50
id: 50
title: How to setup git repository
url: /programming/git/setup-git-repository/
---

## How to setup git repository

11 steps you need to follow to setup a git repository privately as a non root user on linux. I am going to cover how to do this on a RedHat Enterprise Linux Server as this is a very common OS for companies needing service level agreements.

This guide assumes that git is already installed on the network, and that it is accessible from the user you are using on the machine you want to perform the setup on.  Git will work over NFS, so you can follow this guide if your system using the network file system to access git.

In this guide, there will be one or more users working on local copies of the code, and there will be a remote user ( foouser ) on a target machine ( remote1 ) that will host the private repository that will be the remote.

Please follow these steps to setup git repository privately on an internal network.

  1. Create SSH keys for each user that will be accessing this private git repository.
  2. Copy the public ssh keys of each user over to the users directory on the target machine and concatenate them onto the authorized keys file.
  3. If you are using c shell as the system default, make sure to add the location of the git binary to the PATH environment. You can do this by adding a setenv line to the .cshrc file of the user on the machine you are setting the git repository up on.
  4. Create a sub directory called git off of the home directory of the user hosting the remote repository on the target machine.
  5. Change into that directory and create your first project .  Please note that the project directory under the git sub directory must end its directory name in .git.  Lets pretend that I am setting up a project for a Perl module Prolog::Utility::FromPerl  I would create a called Prolog-Utility-FromPerl.git with the following command 
    <pre>git init --bare Prolog-Utility-FromPerl.git</pre>

  6. Now as one of your other users on their local machine create a directory where you will do all of your local development, I just use the same directory name git.  Then under this directory create a directory for your Perl module project called Prolog-Utility-FromPerl without the .git ending
  7. Change into that directory cd ~/git/Prolog-Utility-FromPerl/ and run the following command.  In this command, the name of the remote target machine that will host the remote git repository is called remote1 and the username with the remote git directory is called foouser. 
    <pre>git init && git remote add origin foouser@remote1:/home/users/foouser/git/Prolog-Utility-FromPerl.git</pre>

  8. Now on your local machine create the first file under your local project directory ~/git/Prolog-Utility-FromPerl/ let&#8217;s assume you create a README.txt file with your favorite editor.
  9. After saving the file, run the following commands to commit the file to your local git repository 
    <pre>git add README.txt</pre>
    
    Then
    
    <pre>git commit -m "initial commit of README"</pre>

 10. Now let&#8217;s push your local changes to the remote git repository you setup with the following command 
    <pre>git push origin master</pre>

 11. Finally lets clone this new project with a different user that you setup in step 1 on a different local machine with the command 
    <pre>git clone foouser@remote1:/home/users/foouser/git/Prolog-Utility-FromPerl.git</pre>

Typing out these really long paths can get a bit tedious, so I would recommend that you setup
  
some shortcut aliases in your git config file to make your use of git more productive. If you need some help doing this, please leave me a comment, and I can write a guide on the most useful git shortcuts and aliases to put in your .gitconfig file

To learn more about git, there is a great free online book for learning git called <a href="https://www.git-scm.com/book/en/v2" target="_blank" rel="nofollow">Pro Git</a> that you can reference.