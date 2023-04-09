---
layout: post
title:  "Arrays and Slices in Go: Understanding the Differences"
date:   2023-04-09 10:00:00 +0545
categories: go
---
###Arrays 

when defining array in Go we also have to specify the size of the array or we can use `[...]` during array declaration so the Go complier itself can find the size of the array.

eg. if you are creating an array of 4 you can do it like this:

> [4]string{"zero","one","two","three"} or
> [...]string{"zero","one","two","three"}

if you put nothing in between square brackets Go will create an `Slice`, We will be talking about slice in a while.

Charactertics/limitation of array in Go:

You cannot change the size of an array after you create it.
When you pass an array to a function, it creates an duplicate array inside the function and the data manipulation takes place inside that function only changes the duplicate array and the original array remains unchanged.

Weird Right? but Go has another data type called slice which solves most the issue we face with array.

###Slices

Slices in Go are a bit powerful then array because they are dynamic in nature and can grow or shink according to the requirement and any changes you make to a slice inside a function also affect the original slice because all parameter that gets passed in Go are passed by value.
A slice value is a header that contains a pointer to an underlying array where the elements are actually stored, A side effect of passing the slice header is that it is faster to pass a slice to a function because Go does not need to make a copy of the slice and its elements, just the slice header.

#####creating slice:

you can create slice using `make()` or just like creating array without specifing the size.
If you are creating an empty slice then using make() can be a good choice for you.

> `make([]int,3)` makes a slice of lenght 3 where each element of the slice has value of 0

slice also has another property called `capacity` wich we can find using `cap()`, it tells us about the total capacity of the value slice can hold. If the capacity exceeds we can still add values in the slice using `append()` which also increases the capacity of slice by double.

	slice = make([]string,4) 
	//we created a slice with length 4 so this slice has 4 '0' values elements
	//and this slice has 4 capacity
					
	newSlice[0] = "zero"
	newSlice[1] = "one"
	newSlice[2] = "two"
	newSlice[3] = "three"
	//since the slice had 4 empty values we added values
	//now if we have to add new values we have to use append()
	
	newSlice = append(newSlice,"four")
	
we can also specify capacity of a slice by giving capacity as a third parameter while creating slice

	a := make([]int, 4,8) //a is a slice of lenght 4 and capacity 8
	
Arrays in Go are not very powerful, which is the main reason that Go has
introduced an additional data structure named slice that is similar to an array but
is dynamic in nature. However, data in both arrays and slices is accessed the same way.


