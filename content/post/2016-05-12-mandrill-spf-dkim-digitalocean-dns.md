---
author: Tyson Maly
categories:
- DKIM
- SPF
- DNS
date: "2016-05-12T17:08:11Z"
guid: http://www.tysonmaly.com/?p=700
id: 700
type: archive
title: Mandrill SPF and DKIM on DigitalOcean DNS
url: /mandrill-spf-dkim-digitalocean-dns/
---
Here are some quick tips on setting up SPF and DKIM on digitalocean DNS  for mandrill transactional email

First, mandrill provides an excellent testing for SPF and DKIM, so use it to see if there are any problems with your current settings.

To get started go to the DNS for your domain

To setup the SPF record  choose Add Record

Next choose TXT type

for the name enter: @

for the value enter in quotes:

    "v=spf1 include:spf.mandrillapp.com ?all"

you can add additional includes, but do not include your own domain.  If you are using another service for your smtp and want to add it, only use the root domain e.g.  if your smtp is host701.hostmonster.com  only use  include:hostmonster.com

click the Create button and you should get a success message

Next lets add the DKIM record.  Click Add Record, choose TXT

for the name enter the value: mandrill._domainkey

do not tack on your domain to the end of this, it will not work with the DNS used by digitalocean as it is automatically added.

For the value, enter the key given by mandrill without escaped semicolons, but remember to put the who value in double quotes.

Finally, click Create.

If everything goes well, you should pass both tests on mandrill.
