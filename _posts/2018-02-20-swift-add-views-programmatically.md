---
layout: post
title: Swift Add UIViews programmatically  
categories: [iosDev]
tags : [swift,ios-dev]
comments : true
---

Recently, when i was working on a Swift project on Xcode, i added **UITabBarController** and run the project. When i opened back my storyboard, it was just gone. It threw an error, i tried to figure it out, tested some of the recommended fixes on google, but it could not be solved. Now, i'm 100% implementing my view controllers programmatically.

### Add a basic UIView

I assume that you have just opened a new project and you have your **ViewController.swift** file opened on Xcode. Now we'll add some labels and some other elements to the viewController programmatically.
Let's add a label inside `viewDidLoad()` method : 

```swift
let label = UILabel()
label.translatesAutoresizingMaskIntoConstraints = false
self.view.addSubView(label)
```

This code is clear. We only set the `translatesAutoresizingMaskIntoConstraints` property of the label to `false` cuz we will add our custom constraints programmatically. Let's add them too.

### Add constraints programmatically

We will use the `NSLayoutAnchor` class to define the constraints. There are multiple ways to define a constraint, but this usage is more friendly, more readable in code. As you can guess from the name of the class, we use **anchors** of our UIView element to be contstant at another anchor of another element. You will understand this better in code.

First we need to get the anchors of our super view, which is `self.view`:

```swift
let margins = view.safeAreaLayoutGuide // get the super views anchors

label.leadingAnchor.constraint(equalTo: margins.leadingAnchor).isActive = true // first usage
label.topAnchor.constraint(equalTo: margins.topAnchor, constant: 100).isActive = true // second usage
label.trailingAnchor.constraint(equalTo: margins.trailingAnchor, constant: -20).isActive// third usage
```

Above, there are 3 types of defining a constraint, i wanted show some differences. First usage represents we setting our labels anchor to the views anchor, at same value. Also the `constant:` param value is `0` in this case.

The second line shows the constant parameter usage, which is 100. This means that, set the label's anchor to the views top first, then 100 points below that point.

In the third usage, we setted the right anchor of the label, to the 20 points left from the right of the super view. Assume that the width of the screen is **375**. Then the right point of the label is `375 - 20 = 355`


`viewDidLoad()` final code looks like:

```swift
override func viewDidLoad() {
    super.viewDidLoad()

    let label = UILabel()
    label.translatesAutoresizingMaskIntoConstraints = false
    self.view.addSubView(label)    
        
    let margins = view.safeAreaLayoutGuide // get the super views anchors

    label.leadingAnchor.constraint(equalTo: margins.leadingAnchor).isActive = true // first usage
    label.topAnchor.constraint(equalTo: margins.topAnchor, constant: 100).isActive = true // second usage
    label.trailingAnchor.constraint(equalTo: margins.trailingAnchor, constant: -20).isActive // third usage
}
```

### Conclusion

As it seems, it is quite easy to design your `views` or `viewControllers` programmatically. If you are bored at the opening speed of your storyboards, you can give this a try. If i find time i'll be focusing on this issue more, later.