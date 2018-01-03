---
layout: post
title: Swift Show Alert to User  
categories: [iosDev]
tags : [swift,ios-dev]
comments : true
---

Say that I needed an alert for my app to let the user that my app has some mistakes or you i wanted to user to select some options before moving on, in cases like these you may wanna show a messageBox like alert using the **UIAlertController** class, let's begin

### Initialize class instance

First of all we need an object created from this class:

```swift
var alert : UIAlertController = UIAlertController(title: "Somethings happening", message: "Whadaya wanna do?", prefferredStyle: .alert)
```

Now my alert is ready but it does not have any interactable buttons or something, just an info text. So i want to add and *Ok* button: 

```swift
var action = UIAlertAction(title: "Ok", style: .default, handler: { (action) in
    print("Got it!")
 })

 alert.addAction(alert)
```

Now we just added an *Ok* button.  One thing that you might notice is that the 3rd paremeter of the UIAlertAction constructor method. This is a closure , a void method actually. As you can guess from the parameter name **handler**, we use this method to handle what will happen when the user presses this *Ok* button? So we do not need to name this method and we just printed a log statement in it. Also i need to say that if i would for example, call another method or would try to access a property in my class while in this **closure**, i gotta add `self.` statement before doing so, let's make it clearer :

```swift
// here is my global space in the class
func foo() {

}


func  someFunc() {

        var action = UIAlertAction(title: "Ok", style: .default, handler: { (action) in
        
            print("Got it!")
            self.foo()

    })
}
```

### Add another button : Cancel

Here comes my cancel button that'll dismiss the alert :

```swift
var cancelAction =  UIAlertAction(title: "Cancel", style: .cancel, handler: { (action) in
    self.dismiss(animated: true, completion: nil)
 })
```

You can again see the `self.` statement in my handler closure method. There is also this `completion: nil` statement. This is another method decleraction actually, when that line of coded executed and completed successfully, the method name we sent as parameter to here, will get executed. Since we entered **nil** here, no method or function will be invoked after completion.

That'll be all, thanks. Have a look at the [developer apple portal](https://developer.apple.com) it's quite well written so you almost do not need any other source.