---
author: admintm
categories:
- Computers
- osx
date: "2016-05-16T12:41:41Z"
guid: http://www.tysonmaly.com/?p=175
id: 175
title: Cursor does not appear on startup macbook OSX El Capitan 10.11.4
url: /diy/computers/cursor-does-not-appear-on-startup-macbook-osx-el-capitan-10-11-4/
---

When you startup your macbook, the cursor is invisible or it does not appear on the screen.  I recently updated my macbook pro to El Capitan 10.11.4 and this problem started to appear.

I combed through the system logs and the only thing that stood out to me was

May 16 08:00:12 localhost com.apple.xpc.launchd[1]: assertion failed: 15E65: launchd + 180050 [527954A7-A0F1-305E-B26A-7E632B2CA0FB]: 0x1

but that did not seem to relate to anything specific.

What I did to solve the problem was to hold down the power button till the system powered down.   I then powered the system back up, and the cursor appeared.   I am going to continue to research this for a specific solution.   Right now I believe it is something associated with the update to El Capitan 10.11.14.

&nbsp;

&nbsp;
