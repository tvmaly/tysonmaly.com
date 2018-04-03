---
author: admintm
categories:
- programming
date: "2016-05-17T18:30:24Z"
guid: http://www.tysonmaly.com/?p=184
id: 184
title: How to split pdf into multiple files
url: /programming/how-to-split-pdf-into-multiple-files/
---

## Split pdf files into single page pdf files with this free tool

Here is a quick tip on how you can split pdf files with multiple pages into single page pdf files on windows using a free command line utility called the <a href="https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/" target="_blank" rel="nofollow">pdf toolkit</a>  pdftk by pdflabs.

Say you have a large number of paper documents that you want to scan then extract the text from.  Adobe Acrobat Professional offers the ability to batch process a folder of pdf files and OCR them and extract the text from them.   You can use the Action Wizard to setup the action that will save the PDF files in a folder to text files.

Before you can do this however, you will need to first scan the paper files to PDF.   You will probably want to scan the paper documents in large batches to save time.  If your documents happen to be a fixed number of pages each, you can scan them all at once and then split out the pages using the pdf tool kit.

I am assuming you have already installed the pdf toolkit.  If not, follow the link above that I mentioned to get the free version for windows.  It supports windows XP, Windows 7,  Windows 8, and Windows 10.  If you are running  Mac OSX or Linux Redhat there is a server version that can do the same thing <a href="https://www.pdflabs.com/tools/pdftk-server/" target="_blank" rel="nofollow">here</a>.

We will assume you have a 5 page pdf that is named test.pdf for this example and that you want the each page in its own output file named   test\_01.pdf test\_o2.pdf &#8230;  test_05.pdf   where 01 represents page 1 and 05 represents page 5.

Here are the steps:

  1.  Create folder and copy your batch pdf files to it.
  2.  Open up the command line by running cmd.exe
  3.  Change directories to the folder containing your test.pdf file
  4.  Run the command:  pdftk.exe test.pdf burst test test_%02d.pdf
  5.  Check your folder, you should have test\_01.pdf through test\_05.pdf now.

&nbsp;

The pdf toolkit is a very powerful free tool that has many other uses.

&nbsp;

&nbsp;