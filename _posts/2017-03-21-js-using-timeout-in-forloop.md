---
layout: post
title: Js, Using Timeout in For Loop 
categories: [JavaScript]
tags : [javascript-timeout]
comments : true
---

> Let's say you want to do write numbers from 0 to 10 in a for loop, but you want this to happen after a certain amount of time. Let's do this the old way we know

# Using var keyword

I guess that you'd come up with a solution like this:

{% highlight javascript %}
var counter = 10;
for(var i = 0; i < counter; i++){
    setTimeout(function timer(){
            console.log(i);
        },1000);
}
{% endhighlight %}

The above code should write the numbers in 1 seconds break, but the ouput is not as we expected, it should write **10** ten times. So how is this happening?

## Because of the scope issues

I've been reading *You Don't Know JS* book series,[check it out here it's free to read online](https://github.com/getify/You-Dont-Know-JS), one of them is all about **Scope & Closures**. I learnt that our variable's scope gets stuck in the global scope, or if defined a function, it'd behave the same way, no difference.

What happens is that, our loop iterates **10** times, and because of the scope, the variable `i` holds the value 10, since the loop would end at the value 10 of the variable. 

I mean that our loop does not have a scope itself, so we need to either reassign the value of `i` to another variable. But there is a new way to define variables without `var` keyword.

## let keyword

ES6 introced let keyword, declaring variables with this keyword helps a lot in situations like above. So if i'd just re-produce our code:

{% highlight javascript %}
var counter = 10;
for(let i = 0; i < counter;i++){
   
        setTimeout(function timer(){
            console.log(i);
        },1000);
    
}
{% endhighlight %}

That's it, as i mentioned above you should check out that amazing book, i guess that we don't really know js.