---
author: admintm
categories:
- Python
date: "2014-08-21T13:27:03Z"
guid: http://www.tysonmaly.com/?p=7
id: 7
title: installing textract for python 3
type: archive
url: /installing-textract-for-python-3/
---

I came across this library textract for extracting text from various formats.  I was interested to use this for extracting text from html files.  Here is what I did to get it to install on my machine.

The installation outlines some steps that you need to perform. These steps can be found at the following url:

http://textract.readthedocs.org/en/latest/installation.html

I wanted to install it for python 3.4 on ubuntu 14.04, but it seemed to only support python 2.x.  Here is what I did to get it to install for python 3.4

Get your virtualenv setup first

virtualenv -p /usr/bin/python3.4 /usr/local

1. install required libraries for linux as outlined in the installation page.

2. download the source file for textract from

https://pypi.python.org/pypi/textract

3. untar the downloaded file

4. cd into the directory and look for cases of :

except ShellError,  e:

and change it to

except ShellError as e:

5. edit the requirements/python file comment out

pdfminer==20140328

6. install the python 3 equivalent

pip install pdfminer3k

7. finally run

python3.4 setup.py install

Everything should install at this point.
