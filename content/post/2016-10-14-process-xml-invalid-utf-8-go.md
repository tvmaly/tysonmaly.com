---
author: admintm
categories:
- Go
date: "2016-10-14T21:33:16Z"
guid: http://www.tysonmaly.com/?p=205
id: 205
title: How to process xml with invalid utf-8 bytes in Go including ISO 8859 1 encodings
url: /programming/go/process-xml-invalid-utf-8-go/
---

I recently had to process a large number of xml files that were not UTF-8 encoded.  They also happened to include characters that were outside the valid ASCII range.  I did not really want to keep these invalid characters, and this solution will work for that use case.

If you do need to keep non-ascii characters, this simple solution will not work for you.

The trick to making this work is to create a wrapper around the io.ByteReader that will pre-filter out non-ascii.  Due to how the xml Decoder works, it also expects the wrapper to implement the io.Reader interface.  So here is the code that you can use to perform this filtering.  It assumes you have the asciireader somewhere in your GOPATH and that the file you want to process is called file.xml

<pre>package main

import (
  "log"
  "os"
  "encoding/xml"
  "asciibytereader"
)

func main() {

  file, err := os.Open("file.xml")

  if err != nil {
    log.Fatal(err)
  }

  defer file.Close()

  asciireader := asciibytereader.NewASCIIByteReader(file)</pre>

<pre>decoder := xml.NewDecoder(asciireader)

  // rest of your xml processing code goes here

}
</pre>

### Here is the code for the wrapper that filters out non ascii bytes

<pre>package asciibytereader


import (
    "bufio"
    "io"
)

type ASCIIByteReader struct {
    r *bufio.Reader
    n byte
    e error
    d bool
}

func NewASCIIByteReader(i io.Reader) *ASCIIByteReader {

    return &ASCIIByteReader{r: bufio.NewReader(i), n: byte(0), e: nil}

}

func (a *ASCIIByteReader) Read(p []byte) (n int, err error) {

    n, err = a.r.Read(p)

    return n, err

}

func (a *ASCIIByteReader) ReadByte() (byte, error) {

    if a.d {
        return 0, io.EOF
    }

    for {

        a.n, a.e = a.r.ReadByte()

        if a.e != nil {

            if a.e == io.EOF {
                a.d = true
            }

            return 0, a.e
        }

        if a.n &gt; byte(127) {
            continue
        }

        break
    }

    return a.n, nil

}</pre>