---
author: admintm
categories:
- Security
date: "2016-05-03T12:08:52Z"
guid: http://www.tysonmaly.com/?p=101
id: 101
title: vps security
url: /security/vps-security/
---

# VPS security

Linux security or security in general deals with the process of securing your virtual private server from intrusions and attacks from outside people or agents.  The attack methods may vary and include methods such as password guessing, sql injection attacks, social engineering, and buffer overflows. Security should take a holistic view of the system it is operating on.

## How to secure ubuntu server

I want to discuss how to secure a vps server that is running ubuntu.  Many of these methods will work with other linux distributions.  These steps are used to secure a digital ocean vps, but again they will work on other vps providers.

Step 1:  disable password login over ssh.  You should enable key based login.

Step 2: remove any non essential services such as mail daemons or ftp servers that you do not plan to use.

Step 3: Setup a firewall using iptables, lock down all non essential ports on the machine.  If you are planning on hosting a website with SSL you should only leave port 22 for ssh, port 80 for http, and port 443 for https open.  All other ports should be closed.  Do not use ufw firewall that comes with ubuntu.  I tried to use it once before, and a glitch in ufw caused it to disable the firewall leaving my vps unsecured and open to attach.  Under the hood, ufw uses iptables as the firewall, so it is better to just learn iptables.   If you get this great idea to block ip ranges of entire countries, don&#8217;t do it.  I tried it, but it slows the kernel down so much that the machine is unusable.

Step 4: Install the package <a href="http://packages.ubuntu.com/xenial/iptables-persistent" target="_blank" rel="nofollow">iptables-persistent</a>  using apt-get.  This will remember your iptable firewall rules on restart.

Step 5: Install <a href="http://www.fail2ban.org" target="_blank" rel="nofollow">fail2ban</a> with apt-get.  Fail2ban actively scans logs for patterns of attempted intrusion, and if it finds any, it adds an iptables rule to the firewall to ban the ip address from accessing the vps for a limited time.  An example would be someone trying to login to the vps over ssh with a password multiple time.  You can even setup your own rules when you see certain types of behavior in your /var/log/syslog file

Step 6: <a href="https://help.ubuntu.com/lts/serverguide/automatic-updates.html" target="_blank" rel="nofollow">Setup automatic security updates</a> for Ubuntu.  This will keep your machine up to date automatically with all of the latest security patches for ubuntu.

Step 7: Restart your machine and check that all of the steps 1-6 are still active.