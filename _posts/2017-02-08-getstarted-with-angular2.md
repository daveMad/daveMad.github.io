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

Go back to the terminal/command prompt and you will see it already starts compiling again!


## AppModule

Cd into the *app* folder, and you'll see a file named **app.module.ts**, open it. This is our root module. So, where do we define this is our root module?. In the *src* folder there is a file named **main.ts**. Open it, and at the bottom there is this bootstrapping code:

```javascript
platformBrowserDynamic().bootstrapModule(AppModule);
```

We first import the **AppModule** then bootstrap it. It is our root module. Let's go back to **AppModule**.

{% highlight ts %}

import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

{% endhighlight %}

First we import the ES6 modules that we need to run our app. For example, we import **HttpModule** because we will make HTTP requests to our api. We also import **NgModule** because we need to add some metadata so that it can be known as an Angular Module. There are differences between ES modules and Angular Modules but we'll grasp them in time.

There is a `@NgModule()` above our class. This is a decorator, we'll use them a lot later. We add metadata with this decorator. Let's examine it a little bit;

- declarations array contains the **AppComponent**, but we import it first, then we declare it as our root component
- imports array holds what we imported, they can be angular modules, our own modules, services etc.
- providers array kinda works for the DI(Dependency Injection), let's say we have custom `DataService` and we want to use this service throughout the app, (e.g in other components of the app), so we just provide it here, it becomes **injectable** to the app, and we can use it throughout the app

## AppComponent

In the *src/app/* folder we have a file named **app.component.ts**, open that file. We have a class there named **AppComponent**

We have a decorator above the component. There you will see 3 properties :

### selector

In AngularJS(Angular 1.xx) we were using `ng-app, ng-view` etc. We no longer have these directives. Angular2 has components which manages a section of an html page that we call as **Views**. Selector gives a code to use and reference this component on the html page. Let's how it is used on html side

Open up your index.html. And you will see an html element like this

```html
<app-root>Loading...</app-root>
```

### templateUrl

Go back to your **app.component.ts** file, you'll see the **templateUrl** property. It simply defines our html page that will be rendered on the page that we added our *selector*, which in this case is `<app-root>`.

Open the *app.component.html* file, there is an `<h1>` element there. You can add anything you want, divs, sections, navs, buttons you name it. But don't add tags like `<html> and <body>` because **this is a single page application**, there is onyl one page and the others will be rendered on that page.

### styleUrls

We can also add our specific css files to be used on our component. This is an array property and you can add any number of css files you want


## Conclusion

We've examined our simple app, of course there are many more stuff we gotta look at, like testing, ES6, etc. But i'll write about them later. We don't have to understand every configuration about how the app works, the more we code, we'll understand them better.