---
layout: post
title: Entity Classes in Swift
categories: [iosDev]
tags : [swift,ios-dev]
comments : true
---

We must admit that most of use MVC pattern when it comes to business kinda apps or any type of apps at all. And before developing on Ios i used entity classes with C#, Java, Python you name it, and i want to write an example of them in Swift let's begin.

### Define a new Swift file

I generally store my entity classes in a different folder like, *Model* or *Entities*. Right click in your project navigator, select New File and name your classand press Return key:

```swift
import Foundation
```

You will get this empty swift file, we shall define our class ourselves : 

```swift
...

class BaseEntity {

    init() {

    }
}
```

As you can see there is not much difference to other languages, similar like C# or Java or maybe JavaScript, syntax is pretty cool i guess.

### Add properties to your class

Who does not need properties? Let's add some :

```swift

.... 

    var id : Int
    var name : String

    init(_ id : Int, _ name : String) {
        self.id = id
        self.name = name
    }
....
```

Yep, we defined 2 variables, which've become the class properties now, and we added 2 parameters to our `init()` function, we had to do that if we did not, it would throw an error.

### What if you don't want to define arguments to your init function?

Well that is possible, too. You just need to make your variables **nullable** (aka: nil) :

```swift
...
var id : Int?
var name : String?

init() {

}
...
```

This implementation will not throw an error. 

### Conclusion

This entity class thing almost became a coding standart, wherever you go, you gotta write these in order to keep your code tidy and also they are useful when you work with a database. 