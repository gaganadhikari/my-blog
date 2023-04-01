---
layout: post
title:  "UTF-8 Encoding In Go"
date:   2023-04-01 10:00:00 +0545
categories: go
---
In Go strings are a bit different from what you might be used to. strings are all Unicode in Go and this is because Unicode is used to represent international characters that ASCII simply cannot.

While ASCII (American Standard Code for Information Interchange) represents only American characteristics in 7 bits (0-127), Unicode is capable of representing a much wider range of characters from different languages and scripts. However, this comes at the cost of increased memory usage.

In Go, the length of a string is determined by the number of bytes required to represent the Unicode characters, not the number of Unicode characters. This means that some Unicode characters may require more than one byte to represent.


    package main

    import "fmt"

    func main() {
        s := "énergy"
        fmt.Printf("%T %[1]v %[2]v\n", s, len(s))   // string énergy 7
    }

> Here if we see normally 'énergy' has 6 characters but 'é' is a unicode character,
> which is represented using 2 bits so the length we get is 7


To represent Unicode characters in Go, we use runes. A rune in Go is a 32-bit integer that represents a Unicode code point. However, we don't always represent characters with runes because most of the time, we only work with ASCII characters. Using 7 bits instead of 32 bits can save a lot of memory space, especially when dealing with large strings.

So, how do we represent Unicode characters in Go without using up too much memory? We use UTF-8 encoding. UTF-8 is a way of representing Unicode characters in bytes, and it is a variable-length encoding scheme. This means that Unicode characters that can be represented in a single byte (like ASCII characters) are represented as such, while characters that require more bytes are represented using a sequence of bytes.


    fmt.Printf("%T %[1]v\n", []byte(s))     // []uint8 [195 169 110 101 114 103 121]

    fmt.Printf("%T %[1]v\n", []rune(s))     // []int32 [233 110 101 114 103 121]

> here we can see when we print our string using `UTF-8` encoding it gives us 7 numbers of
> `7 bit` integer and in rune it gives us 6 numbers of `32 bit` integer.
> Simillarly **233** which represents 'é' in 32 bits integer(4 byte) can be repersented
> in 7 bit integer by **195 169**


In conclusion, strings in Go are all Unicode, and we use UTF-8 encoding to represent Unicode characters in bytes. This allows us to work with international characters and scripts without using up too much memory. The length of a string in Go is determined by the number of bytes required to represent the Unicode characters, not the number of Unicode characters, and we can use runes to represent Unicode code points when necessary.