---
layout: post
title: Js, Property Descriptors 
categories: [JavaScript]
tags : [javascript,javascript-property-descriptors]
comments : true
---

> Sometimes you may want your variable to act like a **constant** variable or something, well we can achieve such a behaviour by using **writable property descriptor**

# Object Dot defineProperty

Let's see it in action, first we need an object;

```javascript
var b = {};
```

Then, let's add a property to this objec,we can use the built-in `defineProperty()` function of the `Object` to achieve this :

```javascript
Object.defineProperty(b, "a", {
	value: "b letter",
	writable: false,
	configurable: true,
	enumerable: true
});
b.a; // "b letter"
```

What happened here? We can say that we just changed the characteristics of our object, let's have a closer look:

- The function takes 3 parameters, first is the object that we are going to *modify*.
- Second parameter is our new property name
- The last parameter is an object we use to define the characteristics of our new **property**

To see this in action, press **F12** in your browser then navigate to the **Console** tab, copy & paste this code there, hit enter!

# writable Property

If you saw the second prop, `writable : false`, you'd already guess that we cannot write any other value on that property, which is `b.a`.

Well, what happens if we try to assign another value to it:

```javascript
b.a = 12;
b.a; // "b letter"

```

No errors, no warnings, it just outputs `b letter`. 

# What About const keyword

ES6 introduced a new keyword, `const`. As you can guess we can define constants with it. Let's define a constant:

```javascript
const a = 15;
a; // 15
```

Nothing tricky here, what if we try to re-assign it's value?

```javascript
a = 12;
a; // Error
```

And as we'd expect, it throws an error. I've seen that some engines throw `SyntaxError` while some other engine throws `TypeError`, but the description is same, that we cannot **Re Assign a constant variable**


# configurable Property

Let's have another look at our code :

```javascript
Object.defineProperty(b, "a", {
	value: "b letter",
	writable: false,
	configurable: true,
	enumerable: true
});
b.a; // "b letter"
```

Now we need to figure out what configurable does. Lets change it's value to `false` see what happens:

```javascript
Object.defineProperty(b, "a", {
	value: "b letter",
	writable: false,
	configurable: false, // Notice the false value
	enumerable: true
});
b.a; // "b letter" 

Object.defineProperty(b, "a", {
	value: "a letter",
	writable: false,
	configurable: true, 
	enumerable: true
}); // TypeError
``` 
It's clear that we first declared our property as **un-configurable**, then we tried to configure it again and the engine throws a `TypeError`. 


Lastly, `enumerable` property decides whether or not our property can be defined in an enumerable code block, such as `for` iterations.

# You Don't Know Js: An Amazing Book Series

I've been following [these series](https://github.com/getify/You-Dont-Know-JS) and i've learnt all of these through this book, trust me you should give it a look! 

