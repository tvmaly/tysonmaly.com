---
author: admintm
categories:
- devops
date: "2014-11-30T14:16:05Z"
guid: http://www.tysonmaly.com/?p=13
id: 13
images: [/images/tysonmaly.jpg]
title: fixing php5-fpm logrotate on ubuntu 14.04
url: /devops/fixing-php5-fpm-logrotate-ubuntu-14-04/
---

I was getting an error about the logrotate

    invoke-rc.d: initscript php5-fpm, action "reopen-logs" failed.
    error: error running non-shared post rotate script for /var/log/php5-fpm.log of '/var/log/php5-fpm.log '
    
    

There are two issues, the invoke.d does not seem to have a reopen-logs options, and the logrotate program does not like that systemd has some ownership over /var/log.  To fix these issues, I call the init.d script that has reopen-logs option, and I call the php5 logrotate with the su option at the end.

Here are the changes to  the file /etc/logrotate.d/php5-fpm that work.   You can test them with the command

logrotate &#8211;force php5-fpm

    
    /var/log/php5-fpm.log {
     rotate 12
     weekly
     missingok
     notifempty
     compress
     delaycompress
     postrotate
     /etc/init.d/php5-fpm reopen-logs > /dev/null
     endscript
     su root root
    }
