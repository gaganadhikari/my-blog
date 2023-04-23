---
layout: post
title:  "Packages In Go: Understanding About Code Reusability and Maintainability"
date:   2023-04-23 10:00:00 +0545
categories: go
---
### Package
In Go, a package is a collection of related Go source code files that can be compiled together and used as a unit. Packages are used to organize Go code into reusable and maintainable units. Each package has a unique name that is used to identify it and to refer to its contents from other packages.

Everything in a go lives in package, every go source file starts with a package decelataion.

	package main
	
	import "fmt"
	
	func main() {
		fmt.Println("Hello, world!")
	}
	
Everything in go source code is either a `package scope` or `function scope` 

### Package level decelaration:

If we decelerate anything out of our function before the `main()` function in source file it is inside a package scope.
We cannot use short deceleration operation while declaring package scope `:=` and the deceleration should always starts with a keyword which will makes it easier to parse.

	const AdminID = 69
	var newID string
	
	type user struct{
		...
	}
	
if we think about it alll the function inside a source file is at package scope too.

### Package visibility:

Go uses encapsulation(information hiding) when it comes to packages. when ever we write a package we dont want allow everyone to use everything, some things are kept private to the package. So how do we define things thant can be exported? Its easy, Everyname that starts with a capital letter can be exporetd and used by another package.

	//this cannot be exporetd
	type internal struct {
		...
	}
	
	//this is exportable
	func AllData() {
	}
	
a package usually does not contain a single source file but multiple source files which contains exportable variables and functions.

	fmt.Println()
> ***fmt*** package contains ***Println*** function which can be used by other package
> there are some things that start with lowercase letter inside fmt packgae that are private to the fmt
	
	