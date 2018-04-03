---
author: admintm
categories:
- Programming
date: "2017-09-20T13:22:33Z"
guid: http://www.tysonmaly.com/?p=180
id: 180
title: Perl and Prolog
url: /perl-and-prolog/
---

I just started playing with the perl module Language::Prolog::Yaswi  which allows you to interface with SWI Prolog.   It has a few quirks, but it seems to work well.  I could not get the consult to work as expected using paths outside the current directory.  To get around this limitation, I could simple read the contents of a file located outside the current directory.  Then simple call the swi_inline to consult the code.  Here is an example.

use strict;
  
use IO::File;
  
use Language::Prolog::Yaswi qw(:query :load);
  
use Language::Prolog::Types::overload;
  
use Language::Prolog::Sugar functors => [qw( male female parent father uncle)],
  
vars => [qw (X Y Z)];

my $file = ‘/home/johngalt/pldev/family.pl’;
  
my $fh = IO::File->new($file,”<”) or die($!);
  
my @lines = <$fh>;
  
$fh->close();

swi_inline(@lines);

swi\_set\_query(male(X));

while(swi_next) {
  
printf ” X=%s\n”, swi_var(X);
  
}

<div class="post-info">
</div>
