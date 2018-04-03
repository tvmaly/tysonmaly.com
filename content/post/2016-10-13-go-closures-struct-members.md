---
author: admintm
categories:
- Go
date: "2016-10-13T11:16:41Z"
guid: http://www.tysonmaly.com/?p=202
id: 202
title: Go Closures as Struct Members
url: /programming/go/go-closures-struct-members/
---

How to store closures at runtime inside struct members in the Go programming language.   I will also show you how you can change the closure stored as a member inside of your struct at runtime.   I have used Perl for many years, and you can easily pass around closures and dynamically redefine classes at run time.  You can even create entire classes at run time,  I have done this, and it makes some really interesting patterns.

Doing this in Go is possible, but not as direct as you could in other dynamic programming languages.  The key to remember is that functions are first class in Go.  What that means is that they are treated as any other type.  If you define a new type that represents the function signature you want, then you can store that type as a member in a struct.  Here is an example of how to do this below in golang.  To work within the law of demeter, you could of course add a wrapper method to the Wrap type to call that level of indirection.  As you see below,  I create a closure that I cast of a type of FooFunc when I create an instance of Wrap.  I then test it out in the first two if statements.  After that I decide I want to change the closure inside of the struct to contain a different function at runtime.   You can see this code in action over on the Go Playground at this <a href="https://play.golang.org/p/4bViVV8-4N" target="_blank" rel="nofollow">link</a>.

<pre>package main

import (
    "fmt"
)

type Bar struct {
    Name string
}

// FooFunc is the function I want to assign dynamically in a struct type Wrap
type FooFunc func(b *Bar) bool

type Wrap struct {
    Id             string
    FilterFunction FooFunc
}

// have the type call itself when the Filter method is called
func (f FooFunc) Filter(b *Bar) bool {
    return f(b)
}

func NewWrap() *Wrap {
    filter := func(b *Bar) bool {
        if b.Name == "Foo" {
            return true
        }
        return false
    }

    return &Wrap{Id: "Bestfoodnearme.com", FilterFunction: FooFunc(filter)}
}

func main() {

    w := NewWrap()

    b1 := &Bar{Name: "Foo"}

    b2 := &Bar{Name: "Bar"}

    // call the closure stored in the struct member
    if w.FilterFunction.Filter(b1) {
        fmt.Println("Found a Foo")
    }

    if w.FilterFunction.Filter(b2) {
        fmt.Println("Found a Bar")
    }

    // Change the closure at runtime to be something else
    w.FilterFunction = FooFunc(func(b *Bar) bool {
        if b.Name == "Bar" {
            return true
        }
        return false
    })

    if w.FilterFunction.Filter(b1) {
        fmt.Println("Found a Foo 2")
    }

    if w.FilterFunction.Filter(b2) {
        fmt.Println("Found a Bar 2")
    }

}</pre>