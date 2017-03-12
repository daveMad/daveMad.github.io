---
layout: post
title: Simple Restify & AngularJs App
categories: [AngularJS,Restify]
tags : [angularjs,restify]
---

> For a job application, i was asked to build an SPA app, i wanted to use AngularJS for it's simplicity, and also wanted to include RestifyJs

[View Full Source Code](https://github.com/daveMad/Interview-Sample-App)

I could just build an Angular app, too, but i needed to have some zipcode data of some places, and i found  [this api](https://www.zipcodeapi.com/). They restrict you to use the api, which is only 50 requests in an hour or so. Instead of making get requests each time, i wanted to include some of the initial data in my app.

When planning this, i wanted to use [Restify](http://restify.com/). It's a lightweight RESTful framework (they call it as a module, though), built on Node.js, it's simple and i just wanted to give it a try, instead of [Express](http://expressjs.com/).

So, what i'm gonna do is that i'll have a backend restful service running on node.js, and i'll also have another SPA powered app, and AngularJS app which will make http requests either to my service and to the [3rd party service](https://www.zipcodeapi.com/) to get the data.

# Let's Begin with Restify Service

We have a **dataService.js** file which contains our restify app. I assume that you already typed `npm init` and have your **package.json** file ready. To install restify open up your command line interface, and type the following command :

```bash
npm install restify
```


## Basic Declaration

To have the most basic app you could just navigate their link [here](http://restify.com/#installation). Now let's import the restify & filesystem first:

{% highlight javascript %}
var restify = require('restify');
var fs = require('fs');

{% endhighlight %}

**fs** is a built-in module which can be used to do operations on file system.

{% highlight javascript %}
var server = restify.createServer();
server.use(restify.CORS({ credentials: true }));

server.listen(8080, function () {
    console.log('%s listening at %s', server.name, server.url);
});
{% endhighlight %}

As you can see, it's so simple to start our app. We also  enabled CORS requests for possible CORS issues on line 2.

**server.listen()** takes 2 parameters, first is the port which the app will be serving on, the second is a function callback, that we just inform the user. Because we'll start this using node, we'll be able to see whether the app started or not.


## Let's define the endpoint to get our data

{% highlight javascript %}
function getAllZipcodes(req, res, next) {
    var m = JSON.parse(fs.readFileSync('data.json').toString());
    res.send(m);
};

server.get('/zip', getAllZipcodes);
{% endhighlight %}

**server.get()** just declares that our api has an HTTP GET method. As you can see the first parameter is the route map for it. (e.g : localhost:8080/zip would be convenient) And the second parameter is the callback function

**getAllZipcodes()** function is the callback func that we want to invoke when the user makes a get request. We just read data from a file and parse it into JSON, and finally return the response. We don't have a query parameter, but if we did (e.g: /zip/cityid=Dallas), then we'd have to use it through the **req** parameter. For example, in our function, `req.params.cityid` will return **Dallas** in this case.

For the proper order of the code, see the full **dataService.js** [here](https://github.com/daveMad/Interview-Sample-App/blob/master/server-app/dataService.js)


# AngularJs App, now

Have a look at the [folder here](https://github.com/daveMad/Interview-Sample-App/tree/master/Scripts) which holds our angularjs app. There are four files :

- app.js
- detailController.js
- mainController.js
- zipService.js

## app.js

Lets declare an angularjs  basic app:

{% highlight javascript %}
var app = angular.module('app', ['ngRoute']);
{% endhighlight %}

We declare our app, and add **ngRoute** as our dependency to enable routing/navigation in our app. This a seperate module from the core AngularJs. You can view the docs [here](https://docs.angularjs.org/api/ngRoute)

If you are declaring a brand new app, you have to include the second parameter, i mean the array one. If we did not need to use ngRoute then we'd define our app like this:

`var app = angular.module('app', []);` 

But if you want to access your app which is already defined before then you can do it like:

`var app = angular.module('app');`

Now we should configure our app's routing:

{% highlight javascript %}
app.config(function ($routeProvider) { 
        $routeProvider.when('/home',{
            controller:'mainController',
            templateUrl:'Views/home.html'
        });

        $routeProvider.when('/detail/:zip',{
            controller:'detailController',
            templateUrl:'Views/detail.html'
        });

$routeProvider.otherwise({ redirectTo: '/home' });
{% endhighlight %}

I think it's pretty clear to see what's going on here, but to clarify a little bit:

`$routeProvider.when()` takes 2 parameters, first is the url, the second is a function and in that function, we define our angular controller and the html view page. We'll talk about these a bit later.

`$routeProvider.otherwise()` navigates the unknown url paths to our home view, other than the 2 defined above.


## mainController.js

this controller used to manage our **home.html** page. Let's have a look at it:

{% highlight javascript %}
 var app = angular.module('app');

    app.controller('mainController', function ($scope, zipService, $location) {
        // to do : 
        // - get zipcodes via zipService after load
        // - ng-generate zipcode buttons

        function init() {
            zipService.getZipcodesOfDallas().then(function (response) {
                $scope.zipcodes = response.data.zip_codes;
            }, function (error) {
                alert(error.statusText);
            });
        };

        $scope.goToDetail = function (zip) {
            $location.path('/detail/' + zip);
        };

        init();
});
{% endhighlight %}

First we access to our angularjs app, then we add a controller to it, named as **mainController**. The second parameter is the controller's declaration.

**init()** function simply invokes our angular service's `getZipcodesOfDallas()` function which returns a promise. After having that data, we simply add it to our $scope, if an error occurs we show an alert.

`$scope.goToDetail(zip)` is our router function, to route in an angularjs app, simply inject *$location* built-in service to your controller, and use it's `path(url)` function. Angularjs takes care of everything else.


## detailController.js

Another angularjs controller, it simply injects built-in services and zipService.

{% highlight javascript %}
(function(){
    var app = angular.module('app');

    app.controller('detailController',function($scope,$location,zipService,$routeParams){
        $scope.zip = $routeParams.zip;
        
        (function init(){
            zipService.getLocationByZipcode($scope.zip).then(function(response){
                $scope.zipLocation = response.data;
            },function(error){
                alert(error.statusText);
            });
        }());
    });
}());
{% endhighlight %}


**$routeParams** is important here. In order to get parameters from the router, we use this service. The parameters's name is `zip`, we defined it when configuring our app on **app.js** file. So we simply get the value, then try to get location data via our **zipCodeService** 


## zipService.js

In angular, one of the ways to implement a service is by defining a **factory**. You can read about the services on [official docs here](https://docs.angularjs.org/guide/services)


{% highlight javascript %}
(function () {
    var app = angular.module('app');

    app.factory('zipService', function ($http) {
        var apiBase = 'https://www.zipcodeapi.com/rest/js-lULtvrZBnT2VNJU2iUv21g6kN4ppzqiUk3oQvnrThuP5dK7wECzFSF0GJq6iQodb/info.json/';
        var localApi = 'http://localhost:8080/';
        return {
            getLocationByZipcode: function (zipCode) {
                return $http.get(apiBase + zipCode + '/degrees');
            },
            getZipcodesOfDallas: function () {
                return $http.get(localApi + 'zip');
            }
        }
    });
}());
{% endhighlight %}

We access to our app and  register our service. Similar to the controller definition, first parameter is the service's name ant the second is a function. It just injects the built-in **$http** service, so why do we even need this service?, you may ask. Well, for a more maintainable and modular development, just use these services and if you need to change your back-end api or the endpoints etc., you just have to change one file, your service. Instead of writing the same code on every controller, having a service helps a lot.

It has 2 functions, both of which returns a promise coming from our HTTP requests. I'm returning promise here because it makes it flexible. For example, sometimes you may just want to get a value and sometimes you just want something else, by returning a promise, you can do whatever you want with that data in your controller.

## Html Views

`detail.html` and `home.html` resides in **Views** folder and they have simple definitions. One thing note, we did not define **ng-controller** property to any of our html tags. Since we defined the definitions for the routing in **app.js**, we don't need to use these tags.


# Entry Point, index.html

On the main directory, you should see the `index.html`. We added the references between the `<head>` tags, but we could've added them to the `<body>` tag, either. Also note that the order of the is important, for example if you add **zipService.js** before **app.js** it won't work, same for the angular.js and the angular-route.js

Also we have a directive named **ng-view** on the `<div>` tag, if we don't add this, **routing** the app won't work.


# Running the App

We have 2 apps, one is a node.js app and an angularjs app. We need to run them concurrently, because if we don't run the Restify app, we will not be able to get the data. So let's run it first:

- Open up your cli
- Cd into the **server-app** folder
- Type `node dataService.js`, hit enter

You should see the log on the console that the app's working.


Now we can just open `index.html` and see it in action!

Full Source Code :
https://github.com/daveMad/Interview-Sample-App

Thank you for reading, i know this was a long post but it just happened, keep coding!

