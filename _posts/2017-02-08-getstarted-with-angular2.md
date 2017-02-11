---
layout: post
title: Get Started With Angular 2
categories: [Angular]
tags: [angular2,notes]
---

> Angular2 is a popular Single Page Application framework lately. Before Angular2, there was AngularJS(1.xx) and angular team just call this new Angular2 as **Angular** 


## We are going to set-up a starting project, talk about some important stuff about Angular

What i like about Angular is it's consistency. We seperate every stuff we can, html css and javascript. We have components, which manages a section of an html page, that we call as **Views**. We have modules, services, routing stuff, we have many things to talk about, but i just wanna seperate them and this is gonna be a getting-started post.

## Angular CLI

Google has also built a command line interpreter to ease setup a new Angular application. You can have a look at it's [website](https://cli.angular.io/), it's pretty easy to use it. 

Let's install this cli globally first, open up your command prompt, type :

`npm install -g angular-cli`

npm is a package manager of node.js, if you don't have it you can download [Node.js](https://nodejs.org/en/download/) and it comes with npm installed 

Once we install the Angular cli, now we can bootstrap a new app:

- `ng new angular-initial-project`
- `cd angular-initial-project`

What did we do? We actually now have a brand-new Angular project ready to host. Then, we *cd* into that project folder, and now we can host our app:

`ng serve`

Now, go to `http://localhost:4200/` in your browser and you should see your app working!

# Let's dive deeper

So what happened? It actually installed almost everything we need when developing our Angular app. It even provides a live preview, let's check it out, open up your favorite text-editor, i use Visual Studio Code, and open the project's folder.

There is actually a file named **angular-cli.json** in the root folder, it contains the important configurations of our app. Let's have a look at some of them:

> angular-cli.json

{% highlight js %}
...
 "apps": [
    {
      "root": "src",
      "outDir": "dist",
      "assets": [
        "assets",
        "favicon.ico"
      ],
      "index": "index.html",
      "main": "main.ts",
      "test": "test.ts",
      "tsconfig": "tsconfig.json",
...
""

{% endhighlight %}

 - **root** property's value is src, where our angular app stands
 - **index** points our index.html file, which is entry page of our app
 - **main.ts** is a typescript file, there we bootstrap our application and define our root module
 - **test.ts** is where we keep our tests, we import the required modules and stuff, and use karma to run the tests
 - **tsconfig.json** is holding our compiling configurations


We don't have to understand all of these at the beginning, the more we code, the more we'll get these.


We also have live-preview feature when we use `ng serve`, so to see it in action, i want to change a file. Assuming that you already typed `ng serve` and your app is running on localhost:

- Go to *src/environments/environment.ts*
- Change the *production* value to **true**

Go back to the terminal/command prompt and you will it already starts compiling again!

