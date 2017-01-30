---
layout: post
title: AngularJS Unsupported Media Error
categories: [AngularJS,Notes]
tags : [angularjs,http]
---

So, you made an http request using AngularJs, similar to this : 

{% highlight js %}
$http.post(api, data).then(function(response){

});
{% endhighlight %}

Or maybe a **PUT** request? It does not matter actually, but the original docs does use another snytax like this :

{% highlight javascript %}
$http({
    method : 'POST',
    url : 'api_here'
});
{% endhighlight %}

Let's talk about the problem, it's because you have to add **Content-Type** header value to your request, and it's very easy to add:

{% highlight javascript %}
$http({
    method : 'POST',
    url : 'api_here',
    data : your_data,
    headers : {
        'Content-Type' : 'application/json'
    }  
}).then(function(response){ },function(error){ });
{% endhighlight %}

The error can occur because of an HTTP POST,PUT or DELETE request, adding header should resolve this problem.