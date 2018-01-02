---
layout: post
title: Swifty Notes on Ios Development  
categories: [iosDev]
tags : [swift,ios-dev]
comments : true
---

Hi, i've been a lot busy lately and i could not find time to work on my blog, so new updates here: 
- I've started working on ios apps using swift xcode and stuff
- We had to take a break for game development after publishing 2 games on play store (*search for Eyula*) and now working on our mobile apps (3 app simultaneously) and we are busy, again 

I want to write a bit basics of my Swift development journey, so enough talk here shall we begin?

## Not a so bad language i guess

After working with C#, swift looked like a bit messy but it's moving up in a good situation, i've been using Swift 4 and new to ios development but i feel in the long term it's getting stronger

### Define functions

Sometimes feel like python, sometimes javaScript and even TypeScript but let's have a look at a sample code snippet for swift functions

```swift
func myFunc(number : Int) {
    print(number)
} 
```

Now this is a **void** function. You can also see that we don't have semicolons on lines

Another look at a non-void example:

```swift
func foo(num : Int) -> Int {
    return pow(num, 2)
}
```

Return staments just like in the other popular languages, so notice the `->` statement, makes it a non-void function

### Named parameters

For example if i want to call the above function i'd have to write: 

```swift
foo(num : 49)
```

If i do not add  the **num** then i shall get an error. But this is sick sometimes so to avoid invoking functions like this just define your function in this way:

```swift
func foo(_ num : Int) -> Int {
    return num * num
}

// call it here
foo(49)
```

And boom it should work good. There is this weird style of Swift but im getting used to it. I'll write more about swift at my later posts. Thanks.

