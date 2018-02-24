---
layout: post
title: Swift Anchoring UIScrollViews using NSLayoutAnchor  
categories: [iosDev]
tags : [swift,ios-dev]
comments : true
---

I've been using `NSLayoutAnchor` class to define constraints on my `UIView` controls. But when working with `UIScrollView` i got stuck. It was not scrolling down or up as i add new subViews in it. As it turns out, you need to calculate the spacing between the elements in scrollView, yourself.

### Top Anchor must be set to ScrollViews'

I have a container UIView controller and it's constraints are  set to the **safeArea** like this: 

```swift
let margins = self.view.safeAreaLayoutGuide

let containerView = UIView()
containerView.translatesAutoresizingMaskIntoConstraints = false
self.view.addSubview(containerView)
``` 

I use this container because for `leading and trailing` constraints for my subViews, i will use this container's anchors. Let's define the constraints for it:

```swift
containerView.topAnchor.constraint(equalTo: margins.topAnchor).isActive = true
containerView.bottomAnchor.constraint(equalTo: margins.bottomAnchor).isActive = true
containerView.leadingAnchor.constraint(equalTo: margins.leadingAnchor).isActive = true
containerView.trailingAnchor.constraint(equalTo: margins.trailingAnchor).isActive = true
```

### Initialize UIScrollView instance

ContentSize of scrollView must be set, otherwise it might not be scrolling your elements. We also need to add constraints for it, too;

```swift
let scrollView = UIScrollView()
scrollView.translatesAutoresizingMaskIntoConstraints = false
scrollView.contentSize = CGSize(UIScreen.main.bounds.width, height: 1400)
containerView.addSubview(scrollView)

scrollView.topAnchor.constraint(equalTo: containerView.topAnchor).isActive = true
scrollView.bottomAnchor.constraint(equalTo: containerView.bottomAnchor).isActive = true
scrollView.leadingAnchor.constraint(equalTo: containerView.leadingAnchor).isActive = true
scrollView.trailingAnchor.constraint(equalTo: containerView.trailingAnchor).isActive = true
```

We are done with our scrollView, now we need to add a few elements to it.

### Add random UIView elements

```swift

var fixedHeightOfLabel : CGFloat = 30

for index in 0...18 {
    let label = UILabel()
    label.translatesAutoresizingMaskIntoConstraints = false
    label.text = "Current Label: \(index)"

    scrollView.addSubview(label)

    label.topAnchor.constraint(equalTo: scrollView.topAnchor, constant: CGFloat(index) * fixedHeightOfLabel).isActive = true // we calculate the distance from the top of scrollView, ourselves

    label.leadingAnchor.constraint(equalTo: containerView.leadingAnchor).isActive = true
    label.trailingAnchor.constraint(equalTo: containerView.trailingAnchor).isActive = true
}
```

As you see we need to calculate the distance from the top of scrollView. In another case, let's say you wanna add your label's `topAnchor` right to the bottom of the previous `label`, scrollView won't scroll. That is why we calculate that distance.

Also `leading and trailing` anchors are set to the containerViews'. That is another must, cuz if you set them to the scrollViews', then it won't scroll your labels again. 


### Conclusion

You can combine all the code and add it to your `viewDidLoad()`, it's your choice.

To sum it up,

- Always make sure you provide your `UIScrollView` a contentSize value,
- Do not set subViews leading or trailing anchors, to the scrollViews'
- Calculate the distance yourselves according to `topAnchor` of scrollView.

And you should be good to go!