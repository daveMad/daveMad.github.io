---
layout: post
title: Angular Injectable Services 
categories: [Angular]
tags : [angular,notes]
comments : true
---

When using AngularJS(1.xx), we were defining a service like this:

```javascript
var app = angular.module('app',[]);

app.factory('customService',function($http){
    return {
        getAll:function(){
            return $http.get('Your_Api_Url_Here');
        }
    }
});
```

Well, why do we need to use services? If you don't want to write more code and when you need to change your api, if you don't want to change more code, angular services are your friend.

Generally you'd make http requests but you can use these services for anything, for example if you want to communicate with other components in the app etc.

In Angular 2, there is no so much change, it's simple:
- import the required libs to run the service
- export the service
- make it injectable!

Easy, isn't it? Let's write some code:

```typescript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http'; 

@Injectable()
export class CustomService {
    private apiUrl: string = "Your_Api_Url_Here";

    constructor(private http: Http){}

    getAll(){
        return http.get(apiUrl);
    }
}
``` 

The import statements are required, the annotation `@Injectable()` marks our service as injectable by other components or services. It's almost the same syntax. But there are some other things that may seem strange in a typical JavaScript app.

## Defining http in Constructor

Our constructor takes a paramater of type, `Http`. We included it because we want to make **http** requests to our server, and by defining it like this, angular will inject it into our service. Actually, we could also inject it into our component directly, but like i said, for a more maintainable app we choose to define services.

```typescript
private http: Http
```

To access `Http` service, we defined our local variable named as **http**

```typescript
import { Http } from '@angular/http'; 
```

This import statement is required, we need to import `Http` module so that we can consume it.

## Why Export?

Similar to Es6, when using TypeScript, if you want your module to be consumed throughout the app, you need to **export** it. Without this keyword, any other part of the app won't be able to consume our `CustomService`.

```typescript
export class Consumable { }
```

For more information about exports, please refer [here](https://www.typescriptlang.org/docs/handbook/modules.html#export)

I think that's it for today, i'm planning to write about how to consume these services and how to extend them, soon.
Thanks for reading!

### Useful Links
- [TypeScript Modules](https://www.typescriptlang.org/docs/handbook/modules.html)
- [Angular Documentation About Services](https://angular.io/docs/ts/latest/tutorial/toh-pt4.html)


