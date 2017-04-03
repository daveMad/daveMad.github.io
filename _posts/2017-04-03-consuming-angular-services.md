---
layout: post
title: Consuming Angular Services 
categories: [Angular]
tags : [angular,notes]
comments : true
---

In my previous post, i talked about simple [Angular Services](ly). Now we'll provide these services throughout our app and we'll use their functions in a component.

Let's say we have this service named as `sample.service.ts`:

```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class SampleService{
    private data : Array<any>;

    getUsers(){
        if(this.data === null || this.data.length === 0)
            this.seed();
            
        return this.data;
    }

    private seed(){
        this.data = [
            "Ahmet",
            "Murat",
            "John",
            "Jeffrey",
            "Benjamin"
        ];
    }
}
```

And we want to consume this service, by invoking it from our component. Before doing so, we gotta make sure that our module **provides** this service for us. 

Let's add it to a sample module of our app, named as `app.module.ts`:


```typescript
import {NgModule} from '@angular/core';
import {BrowserModule} from '@angular/platform-browser';
import {FormsModule} from '@angular/forms';

import {AppComponent} from './app.component';


@NgModule({
    declarations: [
        AppComponent
    ]
    imports: [
        BrowserModule,
        FormsModule
    ],
    providers:[
        SampleService
    ],
    bootstrap: [AppComponent]
})
export class AppModule { }
```

So what happened here? Well, this is our **app.module.ts** file, we declared a simple module, actually this is the root module. Did you recognize the `@NgModule` decorator below our class? That is the annotation that makes our class an [Angular Module](ly). In that annotation, there is this `providers: [SampleService]` array. You can add as many as services you want with a comma. 

By adding this `providers` array, we tell our app to make this service (in this case it's `SampleService`)  available through our app. So later we import this service from a component or another service, it'll be injected automatically.

So let's do this in our root component, which is `app.component.ts`:

```typescript
import { Component } from '@angular/core';
import { SampleService } from './sample.service';

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.css']
})
export class AppComponent {
    title = 'app works!';
    users: Array<any> = null;

    constructor(private sampleService: SampleService) {
        this.users = this.sampleService.getUsers();
    }

}
```

Before our service, i want to add something related to these `import` statements. If you see that our import statements does not include the extension of a file, see below:

```typescript
import { SampleService } from './sample.service';
import { AppComponent } from './app.component';
```

If you add the file extension (in this case it is `.ts`), you may get errors like; `Cannot resolve path`. So remember to exclude any file extensions when importing your stuff.

We defined a simple **component**. Added the `@Component()` annotation, defined the selector `app-root` to refer it in our html pages. Then we exported our class, so our module `AppModule` and any other stuff can import it.

We have a null array, that can contain any kinds of data in itself:

`users: Array<any> = null;`

Then we have a constructor, there we aliased our `SampleService` as *sampleService*. You can name it however you want, it's optional. But if you want to use that service, you gotta add it in your constructor, typescript is not the same as javascript. In our constructor function, we invoked the `getUsers()` function of our service and we assigned the result to our array:

```typescript
this.users = this.sampleService.getUsers();
```

Simple, isn't it? I tried to talk about the services, i hope to cover these amazing Angular topics when i got time!
Thanks.

