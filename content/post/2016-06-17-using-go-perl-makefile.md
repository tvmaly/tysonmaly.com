---
author: admintm
categories:
- Go
date: "2016-06-17T15:23:30Z"
guid: http://www.tysonmaly.com/?p=191
id: 191
title: Using Go and Perl in your Makefile.PL as part of your build process
url: /programming/go/using-go-perl-makefile/
---

### Perl and Golang

I want to show you quickly how you can integrate your Go programs into your Perl module process.  That is,  if you have a go executable program that you want to distribute with your Perl module and you also want to build the go executable as part of your Perl module build process, this is how you can do it.

I am assuming you have Go installed, and I am also assuming you are using ExtUtils::MakeMaker for your Perl module.  I also assume that your go binary is installed at  /usr/local/bin/go  but you can change this below if it is somewhere else.

In this example I assume you have a single source file  **script/goprogram.go** within your module code and you want to build an executable **goprogram**

Once you have updated your Makefile.PL  you can simply build your Perl module like you usually do as

perl Makefile.PL

make

make test

make install

If you wanted to get fancier, you could also add in test to run for your go code, but I wanted to keep this example as simple as possible.  I hope you find it useful.

Inside your Makefile.PL  at the bottom add the following lines below:

&nbsp;

<pre>package MY;

sub xs_o {

 my $source = "script/goprogram.go";
 my $executable = "script/goprogram";
 my $gobin = "/usr/local/bin/go";

 my $command = $gobin . " build -o $executable $source";

return &lt;&lt;END
clean :: removego

removego:
\t/bin/touch $executable
\t/bin/rm $executable

all :: buildgo

buildgo:
\t$command
END
}
</pre>

&nbsp;