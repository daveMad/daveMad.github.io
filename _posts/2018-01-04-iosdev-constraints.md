---
layout: post
title: Swift Layout Constraints Basics
categories: [iosDev]
tags : [swift,ios-dev]
comments : true
---

Making your apps look good on any dimension is not quite easy on all platforms, but when developing on xcode, Apple made it easy to make them look fit on any screen size. You achieve this by using **constraints**. Open up your *storyboard* and i assume that you got a few elements on your view and lets a background image.

### Make background fit on all sizes

Your background image should already be in the full-size of the screen, and after doing that, click on the little button right at the bottom of the **pane** (The 2nd button from the right. There are 4 buttons total)

- A popup pane should seem, at the top you got for textviews, the value on all of them should be 0. If not make sure your background image covers all of the screen using drag&drop

- If they are zero, click on the each (*red colored but disabled*) line and so that they seem kinda *enabled*

Now change the viewing mode using **view as** button at the bottom

### Use containers for your elements

A container is actually a view, and these views can be used as parent element for our elements so that we can apply **constraints**  (basically rules) to our ui-elements

- Add a **View** object using the objects-pane at the right bottom pane of xcode

- Make your ui-elements (you can add as many as you want) children of this View

- Your view should be covering your elements, and make your element stand right to some edges of the container view

- Using constraints button, click on red lines again for the touching edges of child & parent elements (it can be right edge and top edge or it can just be the top edge, use it however you want)

    - Make sure that they have value **0** in the textviews

- Click on Add Constraits button and you are done

### Conclusion

Whatever you do, you make sure that your children elements should be touching with and edge of your containers, as long as you use it like this, your elements will be fit on any kind of screen. I actually wrote this as a note to myself but i may write a deeper article about this issue in future posts. Thanks.
