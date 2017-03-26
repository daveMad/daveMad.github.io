---
layout: post
title: this Keyword in JavaScript 
categories: [JavaScript]
tags : [javascript,javascript-this]
comments : true
---

> We happen to guess that the `this` keyword's usage is same to the ones in Java or C# or any other OOP language. But it's not true. I've been following the book series [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS), and i gotta say using `this` is not that easy as it looks.

# What We Normally Assume

We think that it refers to the function that it resides in. For example think about this **C#** code:

{% highlight c# %}

public class Foo
{
    int id;
    public Foo(int id){
        this.id = id;
    }
}

{% endhighlight %}

After using `this` like this, we assume that we can use in a function in **JavaScript** like this:

{% highlight javascript %}
// Global Scope
function foo() {
	console.log( this.a );
}
var a = 2;

foo(); // 2

{% endhighlight %}

Why that logs **2** instead of **undefined** you'd ask, well because `this` does not belong to the enclosing function.

# this Should be Bound to Something

If we bind `this` it should work the way we want. For example, i want `this` refer to my object, how we can achieve this?

{% highlight javascript %}
var obj = {
    a:2
}

function foo(){
    console.log(this.a);
}

foo.call(obj); // 2

{% endhighlight %}

We explicitly bind `this` to refer to my object. You can also use `apply()` instead of `call()`, they do the same work. 

# Using the new Keyword

Normally, we initialize our string or number objects with primitive values, or when defining an object we use (generally) the literal syntax. But if we want to use `this`, we can construct our object using `new` keyword and overrides the mechanism so that we can use `this` safely on our object. 

{% highlight javascript %}
function useNew(a) {
    this.a = a;
}

var obj = new useNew(12);
console.log(obj.a);
{% endhighlight %}


# Using with Arrow-Function

In my previous post i talked about the scoping in a `setTimeout()` function, that it does not have it's own scope, instead it's scope becomes stuck at the global scope. ES6 introduces a new function, **arrow function** and it has it's own scope. If we want to use `this` in an arrow function, we can access to our objects properties: 

{% highlight javascript %}
function foo() {
     for (let index = 0; index < 10; index++) {
        setTimeout(() => {
            this.a += index;
            console.log(this.a);
        }, 100)
    }
}

var obj = {
    a: 2
};

foo.call(obj); // 2, 3, 5, 8 etc.
{% endhighlight %}

Because the arrow-function defines it's own lexical scope, the usage of `this` is achieved. Also, normally the variable `index` value would be stuck at **10**. With using `let` keyword,we solve this problem, too.

# To Sum Up

There are many ways of using `this`, and it's an important part of JavaScript, i'm following the great book series [You Don't Know JS](https://github.com/getify/You-Dont-Know-JS), and if you wanna have a look at more at `this` keyword, you should go for the 3rd book of this series. Thanks for reading.