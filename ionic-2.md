![alt tag](https://github.com/gsoulie/ionic/blob/master/ionic2ban.png)

#ionic 2

> **Warning** this personnal guide is based on the beta of ionic 2. Consequently, some information may be outdated

##### Table of Contents  
* [Prerequisites](#prerequisites)    
	* [Start with ionic](#start-with-ionic)  
	* [Work with Atom editor](#work-with-atom)  
	* [Visual Studio Code](#visual-studio-code)    
* [Concepts](#concepts)    
	* [Angular 2](#angular-2)  
	* [Decorators](#decorators)    	
	* [Pipe](#pipe)    
	* [Promise vs Observable](#promise-vs-observable)    
	* [Mapping](#mapping)    
* [Config](#config)    
* [Global variables](#global-variables)     
* [Third party lib](#third-party-lib)    
* [Useful functions](#useful-functions)  
	* [Get specific platform](#get-specific-platform)    
	* [Show / hide UI elements](#show-hide-ui-elements)    
	* [Checking network connection](#checking-network-connection)    
	* [Close modal](#close-modal)    
* [Moment JS](#momentjs)    
* [File access](#file-access)  
* [Geolocation](#geolocation)  
* [Database](#database)  
	* [SQLite database](#sqlite-database)    
	* [SQLStorage](#sqlstorage)    
* [Camera](#camera)   
* [Gallery](#gallery)    
* [Barcode Scanner](#barcode-scanner)  
* [HTTP query](#http-query)  
* [Navigation](#navigation)  
* [Themes](#themes)  
* [Events](#events)    
	* [Page event](#page-event)    
	* [Event propagation](#event-propagation)    
* [UI Components](#ui-components)    
	* [comboBox](#combobox)    
	* [ion-list](#ion-list)  
	* [searchbar](#searchbar)    
	* [list filtering](#high-performance-list-filtering)    
	* [tab](#tab)       
	* [tab icon](#tab-icon)    
	* [alert dialog box](#alert-dialog-box)    
	* [floating button](#floating-button)  
	* [chart](#chart)    
	* [grid](#grid)    
	* [toggle](#toggle)    
	* [personnal popover menu](#popover-menu)    
	* [dynamic style](#dynamic-style)    
* [Known issues](#known-issues)    
* [Using image](#using-image)    
* [Backends](#backends)    
	* [Strongloop](#strongloop)     
	* [Firebase](#firebase)    
* [Internationalization](#internationalization)  
* [Splash screen and appicon](#splash-screen-and-appicon)  
* [Beta testing](#beta-testing)    
* [Push notification](#push-notification)   
* [Publishing App](#publishing-app)  

#TODO

* AngularJS 2 directive


[TODO](#todo)    

#Prerequisites

##Start with ionic

###Some resources

[link : Good tutorial !!](https://scotch.io/tutorials/build-a-mobile-app-with-angular-2-and-ionic-2)

[link : ng-conf-workshop](https://github.com/chrisgriffith/ng-conf-workshop)    

[link : Official ionic 2 documentation](http://ionicframework.com/docs/v2/getting-started/migration/)

[link : Official ionic 2 native component documentation](http://ionicframework.com/docs/v2/)

[link : ionic 2 project structure](http://ionicframework.com/docs/v2/getting-started/tutorial/project-structure/)

[link : Josh MORONY resources](http://www.joshmorony.com/category/ionic-tutorials/)

[link : Most common ionic mistakes](https://www.toptal.com/ionic/most-common-ionic-development-mistakes)

###Typical installation

**Install / update Node**

First, ensure you have latest version of node

```
$ sudo npm install npm -g
```
**Install cordova**

```
$ sudo npm install -g cordova
```

**Install ionic**

ionic 2 is not yet available in final version, but is it possible to create ionic projects with the ionic 2 beta which can be installed as followed CLI

```
$ sudo npm install -g ionic@beta
```

**Updating ionic 2 framework**

```
$ npm update -g cordova ionic@beta
```

again, and then updating the package.json file of your project. You should see something like 

this in that file:
```
 "dependencies": {
 "angular2": "2.0.0-beta.6",
 "es6-promise": "3.0.2",
 "es6-shim": "0.33.13",
 "ionic-angular": "2.0.0-beta.3",
 "ionic-native": "^1.0.12",
 "ionicons": "3.0.0-alpha.3",
 "reflect-metadata": "0.1.2",
 "rxjs": "5.0.0-beta.0",
 "zone.js": "0.5.14"
 }
```
Simply change the ionic-angular version number to the latest version, and then run:

```
npm install
```


###Configure Android environment variable

```
nano ~/.bash_profile
```

```
export ANDROID_HOME=/Users/gsoulie/Library/android-sdk-macosx
export PATH=${PATH}:/Users/gsoulie/Library/android-sdk-macosx/tools:/Users/gsoulie/Library/android-sdk-macosx/platform-tools
```

**refresh bash_profile**

```
$ source .bash_profile
```

Then, restart your computer and test ANDROID_HOME ```$ANDROID_HOME``` don't forget **$** on the command


###Start with ionic

**ionic 2 project creation**

```
$ ionic start myionic2project --v2 --ts
```

**--ts** to work with TypeScript

**ionic 2 tutorial app**

```
$ ionic start myTutorial tutorial --v2
```

**add platform support to project**

(run it inside you're project folder)

```
$ ionic platform add android
```

**Generate new page in ionic 2 project**

It creates new folder in the project treeview with js, html and scss files

```
$ ionic g page myNewPage
```

**Display log with ionic serve**

```
$ ionic serve -l -s -c
```

```
[--consolelogs|-c] ......  Print app console logs to Ionic CLI
[--serverlogs|-s] .......  Print dev server logs to Ionic CLI
[--port|-p] .............  Dev server HTTP port (8100 default)
[--livereload-port|-i] ..  Live Reload port (35729 default) ========> automatic reload on device
[--nobrowser|-b] ........  Disable launching a browser
[--nolivereload|-r] .....  Do not start live reload
[--noproxy|-x] ..........  Do not add proxies
```

**Testing app on multiple screen sizes and platform**

```
$ ionic serve --lab
```

**Running Emulator**

```
$ ionic build ios
$ ionic emulate ios
```

**Run on device**

After app is running on device, you can inspect it with chrome inspect device

[chrome://inspect/#devices](chrome://inspect/#devices)    

![alt tag](https://s-media-cache-ak0.pinimg.com/originals/8e/52/17/8e5217a74089f046435655d0e0477517.png)


**Installing Gulp**

Gulp is a packet manager for JS libraries. You can use it to add libraries to your Ionic app or to update the Ionic JavaScript library itself.

```
$ sudo npm install -g bower
```

##Work with Atom
[Back to top](#ionic-2) 

[link : best Atom features plugins](https://scotch.io/bar-talk/best-of-atom-features-plugins-acting-like-sublime-text?utm_content=buffer8e88d&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer)     

###1 - Install Atom

[link : Atom website](https://atom.io/)

###2 - Install shell commands

Open your Atom editor and doing

*Main menu -> Install shell command*

It allows you to use ```$ apm``` command to install Atom packages

###3 - Configure Atom auto-updating

```
$ apm install auto-update-packages
```

Next restart Atom

###4 - Useful packages

```
$ apm install atom-typescript
```

```
$ apm install ionic-atom
```

```
$ apm install atom-beautify
```

[link : TODO-show configuration](https://atom.io/packages/todo-show)
```
$ apm install todo-show
```

[link : Minimap configuration](https://atom.io/packages/minimap)
```
$ apm install minimap
```

[link : Linter JSHint](https://atom.io/packages/linter-jshint)
```
$ apm install linter-jshint
```

[link : Linter CSS](https://atom.io/packages/linter-csslint)
```
$ apm install linter-csslint
```

[link : JSDoc](https://atom.io/packages/jsdoc)
```
$ apm install jsdoc
```

[link : Docblockr](https://atom.io/packages/docblockr)
```
$ apm install docblockr
```

[link : merge-conflicts](https://atom.io/packages/merge-conflicts)    

[link : color-picker](https://atom.io/packages/color-picker)    

[link : emmet](https://atom.io/packages/emmet)    



####Activate auto-compilation

[tsconfig.json configuration](https://github.com/TypeStrong/atom-typescript/blob/master/docs/tsconfig.md)    
[Atom typescript plugin documentation](https://github.com/TypeStrong/atom-typescript)    

Create a **tsconfig.json** file in your project root with :

```javascript
{
	"compileOnSave": false
}
```

####Shortcuts

```F6``` For compilation

###Customize colors

To customize Atom editor colors, open Atom preference and on the Settings page, "Open Config Folder". Then, open **style.less** file and add the following code :

```javascript
atom-text-editor::shadow {
  .comment {
    color: #d1cd96;
  }
}
```


##Visual Studio Code
[Back to top](#ionic-2) 

Another very good alternative to Atom is [visual studio code] (https://code.visualstudio.com/c?utm_expid=101350005-27.GqBWbOBuSRqlazQC_nNSRg.2&utm_referrer=https%3A%2F%2Fwww.google.fr%2F)

#Concepts

##Angular 2
[Back to top](#ionic-2)  

[link : become a ninja with Angular 2](https://books.ninja-squad.com/public/samples/Become_a_ninja_with_Angular2_sample.html)    

[link : new Angular 2 concepts and syntax](http://www.joshmorony.com/ionic-2-first-look-series-new-angular-2-concepts-syntax/)    

[link : Angular 2 syntax demistified](http://blog.thoughtram.io/angular/2015/08/11/angular-2-template-syntax-demystified-part-1.html)    

[link : AngularUI](https://angular-ui.github.io/)

AngularJS 2 is the backbone of Ionic 2, is being written for ECMAScript 6

###Some Angular 2 concepts

**Binding a Property to a value**
```xml
<input [value]="firstName">
```

This will set the elements property to fisrtName. More used to see ```{{firstName}}```

**Calling a Function on an Event**

```xml
<button (click)="someFunction($event)">
```

This will call the someFunction function and pass in the event whenever the button is clicked on. You can replace click with any native or custom event you like. You can also use the following syntax:

```xml
<button (^click)="someFunction($event)">
```
to make the event bubble up to other elements.

**Rendering Expressions**

```xml
<p>Hi, {{name}}</p>
```

Just like in Angular 1, this will evaluate the expression and render the result. There’s still some things that are the same!

**Two Way Data Binding**

In Angular 1 we could set up two way data binding by using ng-model, so if we changed a value in an input field with an ng-model it would immediately be updated elsewhere in the application if we were using that value.

We can achieve the same two way data binding in Angular 2 like this:

```xml
<input [value]="name" (input)="name = $event.target.value">
```

This sets the value to the expression name and when we detect the input event we updated name to be the new value that was entered. To make this easier, we can still use ng-model in Angular 2 like this to achieve the same thing:

```xml
<input [(ng-model)]="name">
```

**Creating a Variable to Access an Element**

```xml
<p #myParagraph></p>
```
This creates a local variable that we can use to access the element, so if I wanted to add some content into this paragraph I could do the following:

```xml
<button (click)="myParagraph.innerHTML = 'Once upon a time...'">
```

**Directives**

```javascript
<section *ngIf="showSection">
 
<li *ngFor="let item of items">
```
We can also create embedded templates using directives like ngIf and ngFor.

**Import & Export**

ES6 allows us to Import and Export components. Take the following component for example:

```javascript
import {IonicView, NavController} from 'ionic/ionic';
 
@IonicView({
  templateUrl: 'app/hello-ionic/hello-ionic.html'
})
export class HelloIonicPage {
  constructor(nav: NavController) {
    this.nav = nav;
  }
}
```
This component is making use of the IonicView and NavController components so it imports them. The HelloIonicPage component that is being created here is then exported.

Now you would be able to access HelloIonicPage by importing it elsewhere:

```javascript
import {HelloIonicPage} from './pages/hello-ionic/hello-ionic';
```
It’s a similar concept to Dependency Injection in Angular 1, where we would inject services we were using into the controller like this:

```javascript
.controller('ExampleCtrl', function($scope, $state, $myService) {
```

**Promises**

If you’ve used ngCordova then you will probably already be familiar with promises (a lot of JavaScript libraries implement promises) and why they are easier to use than callbacks. Promises provide a much nicer format for grabbing asynchronous data (e.g. data you need to wait for when you fetch something from a server or device), the current format of callbacks leads to ugly nested code that can become a nightmare to maintain.

ES6 adds native support for promises, which look like this:

```javascript
function msgAfterTimeout (msg, who, timeout) {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve(`${msg} Hello ${who}!`), timeout)
    })
}
msgAfterTimeout("", "Foo", 100).then((msg) =>
    msgAfterTimeout(msg, "Bar", 200)
).then((msg) => {
    console.log(`done after 300ms:${msg}`)
})

this.http.get(url).subscribe(
 (data) => {
 console.log(data);
 },
 (err) => {
 console.log(err);
 },
 () => {
 console.log("completed");
 }
);
```

rather than callbacks which can end up looking like this:

```javascript
function msgAfterTimeout (msg, who, timeout, onDone) {
    setTimeout(function () {
        onDone(msg + " Hello " + who + "!");
    }, timeout);
}
msgAfterTimeout("", "Foo", 100, function (msg) {
    msgAfterTimeout(msg, "Bar", 200, function (msg) {
        console.log("done after 300ms:" + msg);
    });
});
```

**Block Scoping**

Currently, if I define a variable in JavaScript it is available anywhere within the function that I defined it in. The new block scoping features in ES6 allow you to use the new let keyword to define a variable only within a single block of code like this:

```javascript
for (let i = 0; i < a.length; i++) {
    let x = a[i]
    //etc.
}
```
##Decorators
[Back to top](#ionic-2)  

[link : Decorators by Josh MORONY](https://www.joshmorony.com/building-mobile-apps-with-ionic-2/decorators-in-ionic2.html)


####@Component

####@Directive

The @Directive decorator allows you to create your own custom directives. Typically, the decorator would look something like this:

```javascript
@Directive({
    selector: '[my-selector]'
})
```

Then in your template you could use that selector to trigger the behaviour of the directive you have created by adding it to an element:
```xml
<some-element my-selector></some-element>
```
It might be a little confusing as to when to use @Component and @Directive, as they are both quite similar. The easiest thing to remember is that if you want to modify the behaviour of an existing component use a directive, if you want to create a completely new component use a component.

####@Pipe

[link : Understanding Pipe](http://mcgivery.com/understanding-ionic-2-pipe/)

**@Pipe** allows you to create your own custom pipes to filter data that is displayed to the user, which can be very handy. The decorator might look something like this:
```javascript
@Pipe({
  name: 'myPipe'
})
```
which would then allow you to implement it in your templates like this:
```xml
<p>{{someString | myPipe}}</p>
`````
Now someString would be run through your custom myPipe before the value is output to the user.

##Pipe
[Back to top](#ionic-2)  

[link : Understanding Pipe](http://mcgivery.com/understanding-ionic-2-pipe/)      
[link : Josh Morony Pipe documentation](http://www.joshmorony.com/how-to-use-pipes-to-manipulate-data-in-ionic-2/)

###First step : create the pipe class

First, create a "pipe" directory in your project will containing all pipe lib. A basic pipe class looks like below :

```javascript
import {Pipe} from '@angular/core';

@Pipe({
	name: 'helloWorld'	// pipe name
})
export class HelloWorld {
	// Pipe function
	transform(value) {
		return "Hello " + value + "!";
	}
}
```

**Angular 2 best practice**

Always implement the *PipeTransform* interface when building a Pipe

```javascript
export class HelloWorldPipe implements PipeTransform {
	// Pipe function
	transform(value) {
		return "Hello " + value + "!";
	}
}
```

###Using pipe in other page

```javascript
import {HelloWorld} from 'pipes/HelloWorld';	// pipe import

@Component({
	templateUrl: 'myPage/myPage.html',
	pipes: [HelloWorld]	// pipe declaration
})
export class MyPage {
	constructor(){
		this.name = "Andrew";
	}
}
```

**View file**

Pipe inline syntax : ```value | myPipe:args[0]:args[1]```

```xml
<ion-label>{{name | helloWorld}}</ion-label>
```

**Note:** The first letter of the pipe's name in the view file is in lower case

###Other example

**Pipe file**

```javascript
import {Pipe} from '@angular/core';

@Component({
	name: 'addInt'
})
export class AddInt {
	transform(value, args) {
		return value + args[0];
	}
}
```

**Page file**

```javascript
import {AddInt} from 'pipes/AddInt';

@Component({
	templateUrl: 'myPage/myPage.html',
	pipes: [AddInt]
})
export class MyPage {
	constructor(){
		this.myIntArray = [1,3,7,15,31];
		this.mySingleInt = 40;
	}
}
```

**View file**

```
The meaning of life: {{mySingleInt | addInt:2}}

<ul>
<li *ngFor="let myInt of myIntArray">
{{myInt | addInt:1}}
</li>
</ul>
```


###Other example Date format pipe

**Pipe file** (app/pipe/datePipe.js)

```javascript
import {Pipe, PipeTransform} from '@angular/core';

@Pipe({
    name: 'datePipe'  // pipe name
})
/**
 * Formattage de la date en JJ/MM/AAAA
 */
export class datePipe implements PipeTransform{
    // Pipe function
    transform(value) {
        if(value.length == 10){
            return value.substring(8,10) + "/" + value.substring(5,7) + "/" + value.substring(0,4);
        } else {
            return value;
        }
    }
}
```

**Controller file**

**View file**

```javascript
import {datePipe} from '../../pipe/datePipe';

@Component({
  templateUrl: 'build/pages/about/home.html',
  providers: [Utils],
  pipes: [datePipe]
})
export class HomePage {
...

}
```

```xml
...
<ion-label>{{c.dateConso | datePipe}}</ion-label>
...
```



####Conclusion

Pipes are very useful for string formatting like date, hour, regexp...

##Promise vs Observable
[Back to top](#ionic-2) 

[link : RxJS Observables vs Promises](https://egghead.io/lessons/rxjs-rxjs-observables-vs-promises)

Both Promises and Observables provide us with abstractions that help us deal with the asynchronous nature of our applications. However, there are important differences between the two:

- Observable can emit multiple values over time
- Observables can define both the setup and teardown aspects of asynchronous behavior.
- Observables are cancellable.
Moreover, Observables can be retried using one of the retry operators provided by the API, such as retry and retryWhen. On the other hand, 

- Promises will only emit a value once
- Promises require the caller to have access to the original function that returned the promise in order to have a retry capability.

A promise resolves to a single value asynchronously, an observable resolves to (or emits) multiple values asynchronously (over time).

Concrete examples:

- Promise: Response from an Ajax call
- Observable: Click events


For example, **http.get** return Observable, so you must use **subscribe** instead of **then**

```javascript
this.http.get('location/of/data').map(res => res.json()).subscribe(data => {
    console.log(data);
});
```

The code below will not work 

```javascript
this.http.get('location/of/data').then((data) => {
    console.log(data);
});
```

Example : using Promise or Observable

```javascript
var promise = new Promise((resolve) => {
    setTimeout(() => {
        console.log("timeout hit");
        resolve(42);
    }, 500);
    console.log("promise started");
});

promise.then(x => console.log(x));


var source = Rx.Observable.create((observer) => {
    setTimeout(() => {
        observer.onNext(42);
    }, 500);
    console.log("observable started");
});

source.forEach(x => console.log(x));

Instead of Promise, Observable can be cancelled

In the case below, the observable method is cancelled about 500ms.

var source = Rx.Observable.create((observer) => {
    var id = setTimeout(() => {
        observer.onNext(42);
    }, 1000);
    console.log("observable started");

    return () => {
        console.log("dispose called");
        clearTimeout(id);
    }
});

var disposable = source.forEach(x => console.log(x));

setTimeout(() => {
    disposable.dispose();
}, 500);
```
The log output :

> "observable started"
> "dispose called"

If we change timeout value of 500 ms to 1500

> "observable started"
> "42"

#Config
[Back to top](#ionic-2)  

The Config lets you configure your entire app or specific platforms. You can set the tab placement, icon mode, animations, and more here.

[link : Config official documentation](http://ionicframework.com/docs/v2/api/config/Config/)

**sample code of Config**

```javascript
@Component({
  template: `<ion-nav [root]="root"></ion-nav>`
  config: {
    backButtonText: 'Go Back',
    iconMode: 'ios',
    modalEnter: 'modal-slide-in',
    modalLeave: 'modal-slide-out',
    tabbarPlacement: 'bottom',
    pageTransition: 'ios',
  }
})
```

To change the mode to always use Material Design (md).

```javascript
@Component({
  template: `<ion-nav [root]="root"></ion-nav>`
  config: {
    mode: 'md'
  }
})
```

You can also use the config object to define platform specific behaviour:

```javascript
@Component({
  template: `<ion-nav [root]="root"></ion-nav>`
  config: {
    tabbarPlacement: 'bottom',
    platforms: {
     ios: {
       tabbarPlacement: 'top',
     }
    }
  }
})
```

##Mapping
[Back to top](#ionic-2)

In Javascript, mapping is a method available on arrays which allows you to “map” or “transform” each value in that array. Keep in mind that in the example above we are not mapping an array, we are mapping an observable – this functionality is provided by the RxJS library (which is included in Ionic 2 & Angular 2), it is not in Javascript by default.

To give you an example of how normal array mapping works (the concept is basically the same for observables), I could take an array of the following numbers:

**1**
```
[1, 2, 3, 4, 5]
```
and map the array using a function that increments each value by one, which would transform the array into the following:

**2**
```
[2, 3, 4, 5, 6]
```

This would look something like this:
```
[0, 1, 2, 3, 4, 5].map(function(item){
    return item+1;
});
```

We supply map with a function, and then the map will run that function for every value in the array. Whatever we return from that function is what the new value of the item will be – in this case, that is the same number incremented by one. If we instead did something like return 5;, it would turn every value in the array into a 5.

We use map to transform the response into something we can work with. To do that, we create a function that will be applied to each item returned from our observable (which is just the single Response object in this case). The function looks like this:

```javascript
res => res.json()
```

which is shorthand for:

```javascript
(res) => {
    return res.json();
}
```

**Remember** that map is a method that is available on arrays anywhere, it doesn’t need to be inside of an observables map function, and it doesn’t even need to be inside of an Ionic or Angular project

As an aside, filtering and reducing are also available on both observables and arrays, and like map they also return a new observable, so you can create long complex chains like this:

```javascript
this.http.get('location/of/data')
    .map(res => res.json())
    .filter(/*some function*/)
    .reduce(/*some function*/)
    .subscribe(data => {
    console.log(data);
});
```

**filter** can be used to remove values from an array, and **reduce** can be used to calculate some value based on all the values in an array.

```javascript
[0, 1, 2, 3, 4, 5].filter((item) => {
    return item % 2 === 0;
});

//return [0, 2, 4]

['cats', 'kittens', 'puppies', 'dogs'].filter((item) => {
    return item.length < 5;
});

//return ['cats', 'dogs']
```

**Reduce**

Like map and filter, reduce also applies a function to each value in the array, but it doesn’t necessarily result in a new array. Reduce not only supplies you with the value of the current value being operated on, but also the previous value that was returned. This allows you to either compare values in the array, or combine them in some way.

We could create the following reduce function to figure out the highest number in an array:

```javascript
[0, 1, 2, 3, 4, 5].reduce((previous, current) => {
    return Math.max(previous, current);
});
```

The above example compares the current and previous value to see which is higher and then passes that value into the next iteration of the function. The result will be the highest number, which is 5.

We could also figure out the sum of all numbers in the array with the following function:

```javascript
[0, 1, 2, 3, 4, 5].reduce((previous, current) => {
    return current + previous;
});
```
Now with each iteration of the function, the sum of the previous and current will be passe along, resulting in a sequence like:

```
0 + 1 = 1
1 + 2 = 3
3 + 3 = 6
6 + 4 = 10
10 + 5 = 15
```
So, the result of the reduce function will be 15 in this case.

Note that you can also supply an initial value for previous, rather than using the first value of the array, if you add an additional parameter as shown below:

```javascript
[0, 1, 2, 3, 4, 5].reduce((previous, current) => {
    // do something...
}, 5);
```

#Config.xml

[link : ionic doc](http://ionicframework.com/docs/v2/api/config/Config/)

The **config.xml** file allows you to configure a lot of things in your application, like splashscreen duration, screen orientation...

Here are some example :

**Restrict app screen orientation**
```xml
<preference name="orientation" value="portrait"/>
```

**Adjust splashscreen delay**
```xml
<preference name="SplashScreenDelay" value="2000"/>
```

#Global variables
[Back to top](#ionic-2)

Here's a solution to centralize application's globals. The solution consist in using **config.js** file in provider's folder.

You can export all your variable like below :

```javascript
export let VALUE_ONE = "09:00";
export let VALUE_TWO = "192.168.0.1";
...
```

And then in the component or service that requires them, just do this :

```javascript
import {VALUE_ONE} from './config';
```

###Constant

Constant can be declared after lib import like :

```javascript
import {Component} from '@angular/core';
import {NavController, AlertController, ToastController} from 'ionic-angular';
import {Utils} from '../../providers/utils/utils';
import {File} from 'ionic-native';

const fs:string = cordova.file.dataDirectory;
```

#Third party lib
[Back to top](#ionic-2)

##ES6
To use a custom lib file in your project, follow the next steps 

###1 Create "lib" folder under app

```
/app/lib/utils.js
```

###2 implement lib file

ex : utils.js
```javascript
var UI = {};

UI.info = function(_titre, _message){
  _titre = _titre != "" ? _titre : "";
  _message = _message != "" ? _message : "";
  
  console.log(`[--- ${_titre} ---] ${_message}`);
};

export UI;

```
or export only some functions

```javascript
export function getSquare(_value){	// Only this function will be available from external
   return square(_value);
}

function square(_value){	// Not exported
   return _value * _value;
}
```

###3 Using the custom lib in the whole project

ex : From Home.js page
```javascript
import * as UI from '../../lib/utils';

@Component({
  templateUrl: 'build/pages/home/home.html'
})
export class HomePage {

  //Chargement de la base de données
  constructor() {
    UI.info("test","toto"); 
  }
}
```

##TypeScript

###1 Create "lib" folder under app

```
/app/lib/utils.ts
```

###2 implement lib class

ex : utils.ts

```javascript
import {Component, Injectable} from '@angular/core';

@Injectable()
export class UTILS {
    
    constructor() {}
    public info(_elt: string, _msg: string){
        _elt = _elt || "";
        _msg = _msg || "";
        console.log('[--- ' + _elt + ' ---] ' + _msg);
    }
}
````
**Be careful** and don't forget **@Injectable** decorator

###3 Inject class in other component

```javascript
import {UTILS} from '../../lib/utils';

export class HomePage {
	utils: UTILS;
	constructor(){
		this.utils = new UTILS();
		this.utils.info("TEST","my first trace");
	}
}
```

#Useful Functions

##Get specific platform
[Back to top](#ionic-2)  

```javascript
var isWebView = ionic.Platform.isWebView();
var isIPad = ionic.Platform.isIPad();
var isIOS = ionic.Platform.isIOS();
var isAndroid = ionic.Platform.isAndroid();
var isWindowsPhone = ionic.Platform.isWindowsPhone();

var currentPlatform = ionic.Platform.platform();
var currentPlatformVersion = ionic.Platform.version();

platform.isPortrait() 
platform.isLandscape()

-->
/*
window.addEventListener("orientationchange", function() {
    alert(window.orientation);
}, false);*/

ionic.Platform.exitApp(); // stops the app
```
 
##Show hide DOM element
[Back to top](#ionic-2) 

```xml
<button (click)="removeNote()" [hidden]="creationMode">
	<ion-icon name="trash"></ion-icon>
</button>
```

In controller.ts

```javascript
export class HomePage {
  creationMode: boolean = false;
  ... 
}
```


##Checking network connection
[Back to top](#ionic-2)

```
$ cordova plugin add cordova-plugin-network-information
```

```javascript
if(navigator.onLine){
   return true;
} else {
   return false;
}
```

## Close modal
[Back to top](#ionic-2)
	
**View file**
```xml
<button (click)="close()"></button>
```

**Controller file**

Don't forget to import ViewController

```javascript
import { Component } from '@angular/core';
import { NavController,ViewController} from 'ionic-angular';

@Component({
  templateUrl: 'build/pages/route-list/route-list.html',
})
export class RouteListPage {

  constructor(private navCtrl: NavController, private viewCtrl: ViewController) {

  }

  close(){
    this.viewCtrl.dismiss();
  }
}

```

#MomentJS
[Back to top](#ionic-2)  

###Package installation

```
npm install angular-moment moment --save
```

###Usage

```javascript
import * as moment from 'moment';
...
...
let mydate = moment().format('ddd MMM YYYY, h:mm:ss');
```

###Customize locale variables

In the followig example, we define french locale 

```javascript
FR: any = {
    months : "Janvier_Février_Mars_Avril_Mai_Juin_Juillet_Août_Septembre_Octobre_Novembre_Décembre".split("_"),
    monthsShort : "janv._févr._mars_avr._mai_juin_juil._août_sept._oct._nov._déc.".split("_"),
    weekdays : "Dimanche_Lundi_Mardi_Mercredi_Jeudi_Vendredi_Samedi".split("_"),
    weekdaysShort : "dim._lun._mar._mer._jeu._ven._sam.".split("_"),
    weekdaysMin : "Di_Lu_Ma_Me_Je_Ve_Sa".split("_"),
    longDateFormat : {
        LT : "HH:mm",
        L : "DD/MM/YYYY",
        LL : "D MMMM YYYY",
        LLL : "D MMMM YYYY LT",
        LLLL : "dddd D MMMM YYYY LT"
    },
    calendar : {
        sameDay: "[Aujourd'hui à] LT",
        nextDay: '[Demain à] LT',
        nextWeek: 'dddd [à] LT',
        lastDay: '[Hier à] LT',
        lastWeek: 'dddd [dernier à] LT',
        sameElse: 'L'
    },
    relativeTime : {
        future : "dans %s",
        past : "il y a %s",
        s : "quelques secondes",
        m : "une minute",
        mm : "%d minutes",
        h : "une heure",
        hh : "%d heures",
        d : "un jour",
        dd : "%d jours",
        M : "un mois",
        MM : "%d mois",
        y : "une année",
        yy : "%d années"
    },
    ordinal : function (number) {
        return number + (number === 1 ? 'er' : 'ème');
    },
    week : {
        dow : 1, // Monday is the first day of the week.
        doy : 4  // The week that contains Jan 4th is the first week of the year.
    }
};
```

Then, we assign this new locale to moment 

```javascript
moment.locale('fr',this.FR);
...
let formatted = moment().format('dddd D MMMM YYYY'); // will display "jeudi 2 juin 2016"
```


#File access
[Back to top](#ionic-2)  

[link : save image locally](https://forum.ionicframework.com/t/how-to-save-an-image-locally-with-ionic-2/46257/4)

#Geolocation
[Back to top](#ionic-2)  

[link : google map geolocation](http://www.joshmorony.com/ionic-2-how-to-use-google-maps-geolocation-video-tutorial/)

**Adding Google Map API depency in index.html**

```html
<script src="http://maps.google.com/maps/api/js"></script>
<script src="cordova.js"></script>
<script src="build/js/app.bundle.js"></script>
```

**Important** During production deployment, you will have to create Google MAP API key and put it in parameter

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-geolocation
```

**Import the new page in app.core.scss**

```javascript
@import "pages/map/map";
```

**Loading Map (map.html)**


```xml
<ion-header>
	<ion-navbar>
	  <ion-title>
	    Map
	  </ion-title>
	  <ion-buttons end>
	    <button (click)="addMarker()"><ion-icon name="add"></ion-icon>Add Marker</button>
	  </ion-buttons>  
	</ion-navbar>
</ion-header> 
<ion-content>
  <div id="map"></div>  
</ion-content>
```

Next, specify ion-navbar configuration in app.js
```javascript
@Component({
  template: '<ion-nav [root]="root"></ion-nav>',
})

export class AppCmp {
  constructor(platform: Platform){
    ...
    this.root = MapPage;  
  }
}

```

**Updating map.js**

```javascript
import {Component, Geolocation} from 'ionic/ionic';
 
@Component({
  templateUrl: 'build/pages/map/map.html',
})
export class MapPage {
  constructor() {
    this.map = null;
    this.loadMap();
  }
 
  loadMap(){
 
    let latLng = new google.maps.LatLng(-34.9290, 138.6010);
 
    let mapOptions = {
      center: latLng,
      zoom: 15,
      mapTypeId: google.maps.MapTypeId.ROADMAP
    }
 
    this.map = new google.maps.Map(document.getElementById("map"), mapOptions);
  }
}
```

**Styling page (very important) (map.scss)**

```css
.scroll {
    height: 100%;
}
 
#map {
    width: 100%;
    height: 100%;
}
```

**Updating loadMap function**

```javascript
loadMap(){
 
  let options = {timeout: 10000, enableHighAccuracy: true};
 
  navigator.geolocation.getCurrentPosition(
 
      (position) => {
          let latLng = new google.maps.LatLng(position.coords.latitude, position.coords.longitude);
 
          let mapOptions = {
              center: latLng,
              zoom: 15,
              mapTypeId: google.maps.MapTypeId.ROADMAP
          }
 
          this.map = new google.maps.Map(document.getElementById("map"), mapOptions);
      },
 
      (error) => {
          console.log(error);
      }, options
  );
}
```

**Adding marker function (map.js)**

```javascript
addMarker(){
 
  let marker = new google.maps.Marker({
    map: this.map,
    animation: google.maps.Animation.DROP,
    position: this.map.getCenter()
  });
 
  let content = "<h4>Information!</h4>";          
 
  this.addInfoWindow(marker, content);
 
}
```

**Adding addInfoWindow function (map.js)**

```javascript
addInfoWindow(marker, content){
 
  let infoWindow = new google.maps.InfoWindow({
    content: content
  });
 
  google.maps.event.addListener(marker, 'click', function(){
    infoWindow.open(this.map, marker);
  });
 
}
```

#Database

##SQLite database
[Back to top](#ionic-2)  

[link : Using Sqlite storage tutorial](https://devdactic.com/ionic-2-sqlstorage/)

###First solution
There is two main solutions for data storage. The first one is the local HTML5 storage and the second is using SQLite database storage. HTML5 storage provide a key-value storage. This solution can be useful for small applications, but is not adapted for SQL querying. On the other hand, this solution is limitated to 10MB of data storage.

[link : using sqlite](https://www.thepolyglotdeveloper.com/2015/12/use-sqlite-in-ionic-2-instead-of-local-storage/)

This solution using the local device database. **You can make some complex SQL query** for retrieve data.

**Intallation**

After the project is created, intall cordova sqlite storage plugin

```
$ ionic plugin add cordova-sqlite-storage
```

**Database initialization (app.js)**

```javascript
import {App, Platform, Storage, SqlStorage} from 'ionic-angular';
import {HomePage} from './pages/home/home';
import {Component} from '@angular/core';

@Component({
  templateUrl: 'build/app.html',
  config: {}
})
class MyApp {
  static get parameters() {
    return [[App], [Platform]];
  }

  constructor(app, platform) {
    // set up our app
    this.app = app;
    this.platform = platform;
    this.initializeApp();

    // make HelloIonicPage the root (or first) page
    this.rootPage = HomePage;
  }

  initializeApp() {
    this.platform.ready().then(() => {
        this.storage = new Storage(SqlStorage);
        this.storage.query('CREATE TABLE IF NOT EXISTS T_TASKS (id INTEGER PRIMARY KEY AUTOINCREMENT, title TEXT)').then((data) => {
            console.log("TABLE CREATED -> " + JSON.stringify(data.res));//alert("Table créée");
        }, (error) => {
            console.log("ERROR -> " + JSON.stringify(error.err));
        });
   
      if (window.StatusBar) {
        window.Statusbar.styleHex('#A81910');
      }
    });
  }
}
```

**Database manipulation (home.js)**

```javascript
import {App, Platform, Storage, SqlStorage} from 'ionic-angular';
import {Component} from '@angular/core';

@Component({
  templateUrl: 'build/pages/home/home.html'
})

export class HomePage {
    static get parameters() {
      return [[Platform]];
    }

    constructor(platform) {
            this.platform = platform;
            this.cards = [];
            this.platform.ready().then(() => {
                this.storage = new Storage(SqlStorage);
                this.refresh();
            })
        }
   
    add() {

        if(this.title !== ""){
            this.platform.ready().then(() => {
                this.storage.query("INSERT INTO T_TASKS (title) VALUES (?)",this.title).then((data) => {
                    console.log(JSON.stringify(data.res));
                }, (error) => {
                    console.log("ERROR -> " + JSON.stringify(error.err));
                });
            });

            refresh();
        }
    }

    refresh() {
        this.platform.ready().then(() => {
            this.storage.query("SELECT * FROM T_TASKS").then((data) => {
                this.cards = [];
                if(data.res.rows.length > 0) {
                    for(var i = 0; i < data.res.rows.length; i++) {
                        this.cards.push({title: data.res.rows.item(i).title});
                    }
                }
            }, (error) => {
                console.log("ERROR -> " + JSON.stringify(error.err));
            });
        });
    }
}
```
**Displaying data from database (home.html)**

```xml
<ion-header>
	<ion-navbar>
	    <ion-title>
	        Home
	    </ion-title>
	    <button clear (click)="refresh()">Refresh</button>
	    <button clear (click)="add()">Add</button>
	</ion-navbar>
</ion-header> 
<ion-content class="home">
    <ion-list>
        <ion-item *ngFor="let person of people">
            {{person.firstname}} {{person.lastname}}
        </ion-item>
    </ion-list>
</ion-content>
```
##SQLStorage
[Back to top](#ionic-2)  

Is recommanded using **SqlStorage**. 

This is the preferred storage engine, as data will be stored in appropriate app storage, unlike Local Storage which is treated differently by the OS.

**Usage**

```javascript
import {Injectable} from '@angular/core';
import {Http} from '@angular/http';
import {Storage, SqlStorage} from 'ionic/ionic';

@Injectable()
export class Record {
    constructor() {
        this.storage = new Storage(SqlStorage);
        this.storage.set('name','max');
        this.storage.set('lastname','dupont');
    }
    
    createDB(){
	this.storage.query('CREATE TABLE IF NOT EXISTS conso( \
	idConso INTEGER PRIMARY KEY AUTOINCREMENT,  \
	dateConso DATE, \
	tripMax INTEGER, \
	cout REAL, \
	qte REAL, \
	prix REAL, \
	year INTEGER, \
	month INTEGER, \
	dateCreation CHAR(30) \
	)');
    }
    
   addConso(_args: any){
	    
	this.storage.query("INSERT INTO conso (dateConso,tripMax,cout,qte,prix,year,month,dateCreation) VALUES (?,?,?,?,?,?,?,?)",[_args.dateConso, _args.tripMax, _args.cout, _args.qte, _args.prix, _args.year, _args.month, new Date()])
	.then((data) => {
		console.log(JSON.stringify(data.res));
	}, (error) => {
	        console.log("Erreur lors de l'ajout => " + JSON.stringify(error));
	});
  }
}

storage.get('name').then((name) => {

});

// Sql storage also exposes the full engine underneath
this.storage.query('insert into projects(name, data) values("Cool Project", "blah")');
this.storage.query('select * from projects').then((resp) => {})
```

##PouchDB

First, install cordova sqlite-storage plugin

```
$ ionic plugin add cordova-sqlite-storage
```

**TODO - implementing ionic 2 sample app**

####Resources

[Google chrome PouchDB inspector extension](https://chrome.google.com/webstore/detail/pouchdb-inspector/hbhhpaojmpfimakffndmpmpndcmonkfa?hl=en)    

[Ionic 2 - PouchDB tutorial](http://gonehybrid.com/how-to-use-pouchdb-sqlite-for-local-storage-in-ionic-2/)    

#Camera
[Back to top](#ionic-2)  

**include ionic-native package**

```
$ npm install ionic-native --save
```

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-camera
```

**Usage**

View file

```xml
<ion-header>
	<ion-navbar maintheme>
	  <button menuToggle>
	    <ion-icon name="menu"></ion-icon>
	  </button>
	  <ion-title>Photo</ion-title>
	</ion-navbar>
</ion-header>
<ion-content padding class="getting-started">
    <img src="{{sourceImage}}"/>
	<button fab primary fab-bottom fab-center (click)="takePhoto()">
         <ion-icon name="camera"></ion-icon>
    </button>
</ion-content>

```

Controller file
```javascript
import {Component} from '@angular/core';
import {Camera} from 'ionic-native';

@Component({
  templateUrl: 'build/pages/photo/photo.html'
})
export class PhotoPage {
    constructor(){
        this.sourceImage = "";
    }

    takePhoto(){
        let options = {
          quality: 100,
          destinationType: navigator.camera.DestinationType.FILE_URI,
          sourceType: navigator.camera.PictureSourceType.CAMERA,
          encodingType: navigator.camera.EncodingType.JPEG,
          saveToPhotoAlbum: true
        };

        navigator.camera.getPicture(
          (imagePath) => {
            console.log(imagePath);
            this.sourceImage = imagePath;
          },

          (error) => {
            console.log(error);
          }, options
        );
    }
}

```

[link : List of camera options](https://github.com/apache/cordova-plugin-camera#module_camera.CameraOptions)


#Gallery
[Back to top](#ionic-2)  

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-camera
```

**import plugin in ts file**
```javascript
import { Camera } from ‘ionic-native’;
```

**declare image source component**

```javascript
private imageSrc: string;

constructor(private navCtrl: NavController) { }
```

**function to access gallery**

```javascript
private openGallery (): void {
  let cameraOptions = {
    sourceType: Camera.PictureSourceType.PHOTOLIBRARY,
    destinationType: Camera.DestinationType.FILE_URI,      
    quality: 100,
    targetWidth: 1000,
    targetHeight: 1000,
    encodingType: Camera.EncodingType.JPEG,      
    correctOrientation: true
  }

  Camera.getPicture(cameraOptions)
    .then(file_uri => this.imageSrc = file_uri, 
    err => console.log(err));   
}
```

**view file**

```xml
<div class="gallery-button" text-center>
    <img [src]="imageSrc" />    
  <ion-icon name="images" on-tap="openGallery()"></ion-icon>
  <p>Choose a Photo</p>  
</div>
```

**some scss to customize the view**

```css
ion-content, .toolbar-background {
	background-color: #4E8EF7;
	color: #FFFFFF;
}

ion-navbar {
	border-bottom: #FFFFFF 1px solid;
}

.gallery-button {
    bottom: 30px;
    position: absolute;
    width: 100%;    
}

ion-icon[name=images] {	
    border: #FFFFFF 2px solid;    
    border-radius: 50%;
    background-color: #2155AA;    
    font-size: 35px;
		padding: 15px;	
}
 
p {
	font-size: 20px;
}
```

#Barcode scanner
[Back to top](#ionic-2)

[link : Barcode scanner documentation](http://ionicframework.com/docs/v2/native/BarcodeScanner/)

#HTTP query
[Back to top](#ionic-2)  

[link : using http](http://www.joshmorony.com/using-http-to-fetch-remote-data-from-a-server-in-ionic-2/)

[link : reddit API url for testing app](https://www.reddit.com/r/gifs/top/.json?limit=10&sort=hot)

**Create the view (page.html)**

```xml
<ion-header>
	<ion-navbar>
	  <ion-title>Tab 1</ion-title>
	</ion-navbar>
</ion-header>
<ion-content>
  <ion-list>
    <ion-item *ngFor="let post of posts">
      <img [src]="post.data.thumbnail" />
    </ion-item>
  </ion-list>
</ion-content>
```

**Create controller (page.js)**

```javascript
import {Component} from 'ionic/ionic';
import {Http} from '@angular/http';
import 'rxjs/add/operator/map';
 
@Component({
  templateUrl: 'build/pages/page/page.html'
})
export class Page {
  static get parameters() {
     return [[Http]];
  }

  constructor(http) {
 
    this.http = http;
    this.posts = null;
 
    this.http.get('https://www.reddit.com/r/gifs/new/.json?limit=10').map(res => res.json()).subscribe(data => {
        this.posts = data.data.children;
    });
 
  }
}
```

####Note : 
The **map** lib is only imported because we need is http.get function

#Navigation
[Back to top](#ionic-2)  

###Using NavController

[link : Understanding ionic 2 NavController](http://mcgivery.com/understanding-ionic-2-navigation-navcontroller/)

Before we can use the NavController, we will need to import it.

```javascript
import {NavController} from 'ionic-angular';
```

Next we will inject it into our ```@Component``` and assign it to a property.

```javascript
import {Component, NavController} from 'ionic-angular';

@Component({
	templateUrl: "build/pages/Main/Main.html"
})
export class MainPage(){
	constructor(nav: NavController){
		this.nav = nav;
	}
}
```

Now, we can call properties on nav, our instance of **NavController**. For example, say we want to navigate from our Main view to our About view, we would need to start by importing that ```@Component``` class.

```javascript
import {Component, NavController} from 'ionic-angular';
import {AboutPage} from 'About/About'

@Component({
	templateUrl: "build/pages/Main/Main.html"
})
export class MainPage(){
	constructor(nav: NavController){
		this.nav = nav;
	}
}
```

Next, let’s create a method on our page called **goToAbout** that we can call from our template. This method will push the AboutPage onto the stack.

```javascript
import {Component, NavController} from 'ionic-angular';
import {AboutPage} from 'About/About'

@Component({
	templateUrl: "build/pages/Main/Main.html"
})
export class MainPage(){
	constructor(nav: NavController){
		this.nav = nav;
	}
	
	goToAbout(){
		this.nav.push(AboutPage);
	}
}
```

In our template, **Main.html**, we will have a button that will call this method when pressed.

```xml
<button (click)="goToAbout()">About</button>
```

To summarize, when this button is pressed, it will call the goToAbout method which pushes an instance of the AboutPage class onto the navigation stack which is then compiled and animated into view.

####Passing Data
In many scenarios we have data in one view that we need to pass to another. Luckily, the push method accepts a second parameter which is an object of data to pass to the ```@Component``` passed into the first parameter.

```javascript
this.nav.push(AboutPage,{
	username: "andrewmcgivery",
	blogger: true
});
```

This data is then accessible in the pushed ```@Component``` via navParams which is similar to $stateParams in 1.0.

```javascript
import {Component, NavParams} from 'ionic-angular';

@Component({
	templateUrl: 'build/pages/About/About.html',
})
export class AboutPage {
	constructor(navParams: NavParams){
		this.username = navParams.get("username"); // "andrewmcgivery"
		this.blogger = navParams.get("blogger"); // true
	}
}
```
####Pop

Pop is super simple to use as well. As an example, if we wanted to create a function called **goBack** that goes back when pressed in our AboutPage, we could just call **nav.pop()** :

```javascript
import {Component, NavController} from 'ionic-angular';

@Component({
	templateUrl: 'build/pages/About/About.html',
})
export class AboutPage {
	constructor(nav: NavController){
		this.nav = nav;
	}
	
	goBack(){
		this.nav.pop();
	}
}
```

####Other Methods
There is a few more methods available on the NavController such as insert, remove, etc. I would suggest reading the Official Docs.

####Lifecycle Events
In version 1.0, we had the concept of events being fired when we were entering and leaving the view, among others. In version 2.0, we have a very similar set of events. To handle one of these events, we just need to give our ```@Component``` class a method that matches the event. For example, if we want to run an event when the ```@Component``` is loaded, we will need to give our page the **onPageLoaded** method:
```javascript
import {Component} from '@angular/core';

@Component({
	templateUrl: 'build/pages/About/About.html',
})
export class AboutPage {
	onPageLoaded(){
		console.log("Page Loaded!");
	}
}
```

We can have a set of handlers for a variety of events including then the page is about to be entered, when the page is leaving, etc. Again, I would suggest reading the Official Docs.

##Themes
[Back to top](#ionic-2)  

###Statusbar

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-statusbar
```

**Customize**

```javascript
import {Platform} from 'ionic-angular';
import {Component} from '@angular/core';
import {TabsPage} from './pages/tabs/tabs';


@Component({
  template: '<ion-nav [root]="rootPage"></ion-nav>',
  config: {} // http://ionicframework.com/docs/v2/api/config/Config/
})
export class MyApp {
  static get parameters() {
    return [[Platform]];
  }

  constructor(platform) {
    this.rootPage = TabsPage;

    platform.ready().then(() => {
            StatusBar.backgroundColorByHexString("#25312C")
    });
  }
}
```

###Change background color of a specific page

```xml
<ion-content padding class="masters">
  <ion-list inset>
    <button ion-item *ngFor="#master of masterPages" (click)="navMaster(master)">
      {{master.title}}
    </button>
  </ion-list>
</ion-content>
```

Then in your scss you target the class in the ion-content tag:

```javascript
.masters {
  background-color: green;
}
```

Lastly you make sure this scss is being compiled with your **app.core.scss** by importing it in that same file like:

```javascript
@import "../pages/masters/masters";
```

#UI Components

##ComboBox
[Back to top](#ionic-2)  

**View file**
```xml
<ion-item>
	<ion-label>Profession</ion-label>
	<ion-select [(ng-model)]="prof" (ionChange)="selectObject($event)">
		<ion-option *ngFor="let item of professions" value="{{item.objectId}}">{{item.titre}}</ion-option>
	</ion-select>
</ion-item>
```

**Controller file**

```javascript
public prof: string;
private professions: any[];
private newSelectedId: number = 0;

constructor(){
	this.prof = "prof 1";
	this.professions = [{objectId: 1, titre: "prof 1"},{objectId: 2, titre: "prof 2"},{objectId: 3, titre: "prof 3"}];
}

// To verify
selectObject(_selectedItem){
	this.newSelectedId = _selectedItem
}
```

#Events

##Page event
[Back to top](#ionic-2)

| Page event    | Description   |
| ------------- |---------------|
| ionViewLoaded      | Runs when the page has loaded. This event only happens once per page being created and added to the DOM. If a page leaves but is cached, then this event will not fire again on a subsequent viewing. The ionViewLoaded event is good place to put your setup code for the page. |
| ionViewWillEnter      | Runs when the page is about to enter and become the active page.      |
| ionViewDidEnter | Runs when the page has fully entered and is now the active page. This event will fire, whether it was the first load or a cached page.      |
| ionViewWillLeave | Runs when the page is about to leave and no longer be the active page. |	
| ionViewDidLeave | Runs when the page has finished leaving and is no longer the active page. |
| ionViewWillUnload | Runs when the page is about to be destroyed and have its elements removed. |
| ionViewDidUnload | Runs after the page has been destroyed and its elements have been removed. |

##Event propagation
[Back to top](#ionic-2)  

This code show how to stop event propagation

**View file**

```xml
<ion-content padding class="page1">
  <ion-list>
    <ion-item *ngFor="let item of items" (click)="openDetail(item.idDevice, item.nom)">
      <button clear item-right (click)="pickDevice($event,item.idDevice)">
        <ion-icon green name="phone-portrait" item-right></ion-icon>
      </button>
      <h2>{{item.nom}}</h2>
    </ion-item>
  </ion-list>
</ion-content>
```

**Controller file**

```javascript
pickDevice(event,_idDevice){
    event.stopPropagation();
  }
```


##ion-list
[Back to top](#ionic-2)  

Standard dynamic ion-list item

```xml
<ion-list> 
    <ion-item *ngFor="let item of items">{{item.fullname}}</ion-item> 
</ion-list>
```

For clickable list you have to use **button ion-item**

```xml
<ion-list> 
    <button ion-item *ngFor="let item of items">{{item.fullname}}</button> 
</ion-list>
```

###Add filter on ion-list

Consider a ion-list in which we want to hide every items which property "deleted" is set to true

```xml
<ion-list>
  <ion-item-sliding *ngFor="let item of getActiveItems()" #slidingItem>
    <ion-item>{{item.fach}} ({{item.kuerzel}})</ion-item>
    <ion-item-options>
      <button (click)="showEditModal(item, slidingItem)"><ion-icon name="create"></ion-icon>Bearbeiten</button>
      <button danger (click)="doConfirm(item, slidingItem)"><ion-icon name="trash"></ion-icon>Löschen</button>
    </ion-item-options>
  </ion-item-sliding>
</ion-list>
```

```javascript
@Component(
    // ...
)
export class TestPage {
    // ...
    getActiveItems() {
        // NOTE: Returning a new array might mess up the change detection of Ng2.
        // TODO: Use an existing array instead of returning a new one each time.
        return this.items.filter(item => !item.deleted);
    }
}
```

Second solution, in case that you prefer to do the filtering in the template then you can do it this way:

```xml
<ion-list>
  <template ngFor #item="$implicit" [ngForOf]="items">
    <ion-item-sliding *ngIf="!item.deleted" #slidingItem>
      <ion-item>{{item.fach}} ({{item.kuerzel}})</ion-item>
      <ion-item-options>
        <button (click)="showEditModal(item, slidingItem)"><ion-icon name="create"></ion-icon>Bearbeiten</button>
        <button danger (click)="doConfirm(item, slidingItem)"><ion-icon name="trash"></ion-icon>Löschen</button>
      </ion-item-options>
    </ion-item-sliding>
  </template>
</ion-list>
```


###Remove item from list

**View file**
```xml
<ion-list>
    <ion-item-sliding *ngFor="let post of posts">
    	<ion-item>
    	...
    	</ion-item>
    	<ion-item-options>
    	    <button danger (click)="removePost(post)">
    	    	<ion-icon name="remove"></ion-icon>
    	    </button>
    	</ion-item-options>
    </ion-item-sliding>
</ion-list>
```

**Controller file**

```javascript
removePost(post){
    let index = this.posts.indexOf(post);

    if(index > -1){
      this.posts.splice(index, 1);
    }
}
```

###ion-item-sliding

```xml
<ion-content class="home">
  <ion-list>
    <ion-item-sliding  *ngFor="#item of notes" >
      <button ion-item (click)="noteSelected(item)">
        <ion-item-content>
          <h2>{{item.title}}</h2>
          <p>{{item.text | truncate: 20}}</p>
        </ion-item-content>
      </button>

      <ion-item-options>
        <button darkgrey (click)="removeNote(item)" class="btn"><ion-icon name="trash"></ion-icon>Delete</button>
      </ion-item-options>
    </ion-item-sliding>
  </ion-list>
</ion-content>
```

###Inifinite scroll in ion-list

####Solution 1

[link : Scroll performance](http://www.joshmorony.com/boosting-scroll-performance-in-ionic-2/)
[link : virtual-scroll official doc](http://ionicframework.com/docs/v2/api/components/virtual-scroll/VirtualScroll/)

**Create new project**

```
ionic start virtual-scroll tabs --v2
```

**Create Data**

Modify Page1 and Page2 controller with :

```javascript
import {Component} from '@angular/core';

@Component({
  templateUrl: 'build/pages/page1/page1.html'
})
export class Page1 {
  constructor() {
 
    this.items = [];

    for(let i = 0; i < 2000; i++){

        let item = {
            title: 'Title',
            body: 'body',
            avatarUrl: 'https://avatars.io/facebook/random'+i
        };

        this.items.push(item);
    }

  }
}
```

**Create List**

First we’re going to set up a standard list to display the data we created in the constructor.

Modify **page1.html** to reflect the following:
```xml
<ion-header>
	<ion-navbar>
	  <ion-title>
	    Standard Scroll
	  </ion-title>
	</ion-navbar>
</ion-header> 
<ion-content class="page1">
 
  <ion-list>
    <ion-item *ngFor="let item of items">
      <ion-avatar item-left>
        <ion-img [src]="item.avatarUrl"></ion-img>
      </ion-avatar>
 
      <h2>{{item.title}}</h2>
      <p>{{item.body}}</p>
    </ion-item>
  </ion-list>
</ion-content>
```

In this case we are just using the standard ```*ngFor``` directive to loop over all of the items in our array and create list items for them. Since we are not using virtual scroll, **this means that DOM elements are going to be created for every single item !**. If you try to run the application now, you will likely even notice there is a considerable amount of lag just in loading the app.

**Create a Virtual Scrolling List**

Now we’re going to create a list that uses virtual scroll.

Modify **page2.html** to reflect the following:

```xml
<ion-header>
	<ion-navbar>
	  <ion-title>
	    Virtual Scroll
	  </ion-title>
	</ion-navbar>
</ion-header> 
<ion-content class="page2">
    <ion-list [virtualScroll]="items">
 
      <ion-item *virtualItem="let item">
        <ion-avatar item-left>
          <ion-img [src]="item.avatarUrl"></ion-img>
        </ion-avatar>
 
        <h2>{{item.title}}</h2>
        <p>{{item.body}}</p>
      </ion-item>
    </ion-list>
</ion-content>
```
The syntax is a little different, this time we are using [virtualScroll] and *virtualItem, but the concept is the same. We are setting up some data that will be looped over for the list. The only difference now is that this list will now use virtual scrolling instead of the standard scrolling.

It’s important for the virtual scroll to know approximately how big your items will be, since it needs to know how many items would be required to fill up the screen. You can help this process by specifying an approxItemWidth and approxItemHeight

####Solution 2

[link : Infinite scroll](http://ionicframework.com/docs/v2/api/components/infinite-scroll/InfiniteScroll/)

View file
```xml
<ion-content>
 <ion-list>
   <ion-item *ngFor="let i of items"></ion-item>
 </ion-list>

 <ion-infinite-scroll (infinite)="doInfinite($event)">
   <ion-infinite-scroll-content
      loadingSpinner="bubbles"
      loadingText="Loading more data...">
    </ion-infinite-scroll-content>
 </ion-infinite-scroll>
</ion-content>
```

Controller file
```javascript
@Component({...})
export class NewsFeedPage {

  constructor() {
    this.items = [];
    for (var i = 0; i < 30; i++) {
      this.items.push( this.items.length );
    }
  }

  doInfinite(infiniteScroll) {
    console.log('Begin async operation');

    setTimeout(() => {
      for (var i = 0; i < 30; i++) {
        this.items.push( this.items.length );
      }

      console.log('Async operation has ended');
      infiniteScroll.complete();
    }, 500);
  }
}
```

###Set colour dynamically of each ion-item

**View file**

```xml
<ion-list>
	<ion-item *ngFor="let item of items" (click)="openDetail(item.idDevice, item.nom)">
		<button clear item-right (click)="pickDevice($event,item.idDevice)">
			<ion-icon [style.color]="item.disponible ? '#00CC00' : '#CD1625'" name="phone-portrait" item-center></ion-icon>
		</button>
		<h2>{{item.nom}}</h2>
	</ion-item>
</ion-list>
```

**IMPORTANT** It's important to set colour by using hexadecimal string instead of standard colour name like 'primary', 'danger' etc... because it's actually doesn't work.

**Controller file**

```javascript
export class Page1 {
  public items: any[];

  constructor(public nav: NavController) {
    this.nav = nav;

    let dataset = [{
      idDevice: "1",
      nom: "iPhone 4S",
      disponible: true
    },{
      idDevice: "2",
      nom: "iPad2",
      disponible: true
    },{
      idDevice: "3",
      nom: "Mac Mini 1",
      disponible: false
    },{
      idDevice: "4",
      nom: 'Mac Book Pro 17"',
      disponible: false
    },{
      idDevice: "5",
      nom: "Nexus 4",
      disponible: true
    }];

    this.items = dataset;
  }

  openDetail(_idDevice, _deviceName){
    this.nav.push(FichePage,{idDevice: _idDevice, deviceName: _deviceName});
  }
}
```

**Change button backgroundColor synamically**

```xml
<button [style.backgroundColor]="enable ? '#00CC00' : '#FF0000'">Test</button>
```


###Pull to refresh

**In your html file**

```xml
<ion-content padding>
  <ion-refresher (ionRefresh)="doRefresh($event)">
    <ion-refresher-content></ion-refresher-content>
  </ion-refresher>
  <ion-list>
    <button ion-item *ngFor="let user of users" (click)="goToDetails($event, user.login)">
      <ion-avatar item-left>
        <img [src]="user.avatar_url">
      </ion-avatar>
      <h2>{{ user.login }}</h2>
      <ion-icon md="md-arrow-forward" item-right></ion-icon>
    </button>
  </ion-list>
</ion-content>
```

**In your controller file**

```javascript
doRefresh(refresher){
    this.users = getUsers();
    setTimeout(() => { refresher.complete(); console.log('Async operation has ended'); }, 2000); 
  }
```

##Searchbar
[Back to top](#ionic-2)  

**View file**
```xml
<ion-header>
  <ion-navbar primary>
    <ion-title>
      Annuaire
    </ion-title>
  </ion-navbar>
  <ion-toolbar maintheme>
  <ion-searchbar placeholder="Rechercher un device" (ionInput)="getDevice($event)"></ion-searchbar>
   </ion-toolbar>
</ion-header>

<ion-content padding class="page1">
  <ion-list>
    <ion-item *ngFor="let item of items">
      <h2>{{item.nom}}</h2>
    </ion-item>
  </ion-list>
</ion-content>

```

**Controller file**
```javascript
constructor(public nav: NavController) {
    this.nav = nav;
    this.getAllDevices();
  }

  getAllDevices(){
    this.items = [{
      nom: "iPhone 4S",
      version: "iOS 7.2.1"
    },{
      nom: "iPad2",
      version: "iOS 8.3"
    },{
      nom: "Mac Mini 1",
      version: "Mac OSX El Capitan - SSD 128Go"
    },{
      nom: 'Mac Book Pro 17"',
      version: "Mac OSX Yosemite"
    },{
      nom: "Nexus 4",
      version: "Android 4.4.4"
    }];
  }
  
  getDevice(ev: any){
    this.getAllDevices();

    // set searchText to the value of the searchbar
    var searchText = ev.target.value;

    // Avoid research if searchtext is empty
    if (!searchText || searchText.trim() === '') {
      return;
    }

    // Filtering on the attribute 'nom'
    this.items = this.items.filter((v) => {
      if (v.nom.toLowerCase().indexOf(searchText.toLowerCase()) > -1) {
        return true;
      }
      return false;
    })
  }
```

##High performance list filtering
[Back to top](#ionic-2)  

To increase list filtering, we can use Observable instead of basic filtering shows in searchbar section above.

**View file**

```xml
<ion-header>
  <ion-navbar primary>
    <ion-title>
      Ionic Blank
    </ion-title>
  </ion-navbar>
</ion-header>
 
<ion-content class="home-page">
 
    <ion-searchbar [(ngModel)]="searchTerm" [formControl]="searchControl" (ionInput)="onSearchInput()"></ion-searchbar>
 
    <div *ngIf="searching" class="spinner-container">
        <ion-spinner></ion-spinner>
    </div>
 
    <ion-list>
        <ion-item *ngFor="let item of items">
            {{item.title}}
        </ion-item>
    </ion-list>
</ion-content>
```

**Controller file**
```javascript
import { Component } from '@angular/core';
import { Control } from '@angular/common';
import { NavController } from 'ionic-angular';
import { Data } from '../../providers/data/data';
import 'rxjs/add/operator/debounceTime';
 
@Component({
  templateUrl: 'build/pages/home/home.html',
  providers: [Data]
})
export class HomePage {
 
    searchTerm: string = '';
    searchControl: Control;
    items: any;
    searching: any = false;
 
    constructor(public navCtrl: NavController, private dataService: Data) {
        this.searchControl = new Control();
    }
 
    ionViewLoaded() {
        this.setFilteredItems();
 
        this.searchControl.valueChanges.debounceTime(700).subscribe(search => {
            this.searching = false;
            this.setFilteredItems();
        });
    }
 
    onSearchInput(){this.searching = true;}
 
    setFilteredItems() {this.items = this.dataService.filterItems(this.searchTerm); }
}
```

**Style file**

```css
.home-page {
 
    .spinner-container {
        width: 100%;
        text-align: center;
        padding: 10px;
    }
 
}
```

**Data.ts provider**

```javascript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';
import 'rxjs/add/operator/map';
 
@Injectable()
export class Data {
    items: any;
 
    constructor(private http: Http) {
        this.items = [
            {title: 'one'},
            {title: 'two'},
            {title: 'three'},
            {title: 'four'},
            {title: 'five'},
            {title: 'six'}
        ]
    }
    filterItems(searchTerm){
        return this.items.filter((item) => {
            return item.title.toLowerCase().indexOf(searchTerm.toLowerCase()) > -1;
        });     
    }
}
```


Our list filtering is designed pretty nicely now, and it should perform very well. However, since we have added this debounceTime it causes a slight delay that will certainly be perceptible to the user. Whenever we do something “in the background” we should indicate to the user that something is happening, otherwise it will appear as if the interface is lagging or broken.

A delay is fine, and an artificial delay is sometimes even beneficial, but you definitely don’t want to leave the user wondering “is this just slow or is it frozen?”.

We’re going to make a change now that won’t have any effect on performance, but it will have an impact on the user’s perception of the responsiveness of the app. We’re simply going to add a loading spinner that will display when a search is in progress.

##Tab
[Back to top](#ionic-2)  

According to the latest Android material guideline, you have to follow these rules :

- 3 to 5 destinations => use the bottom navigation
- Less than 3 => use tab on the top
- More than 5 => use another solution like slide menu

So, by default, ionic 2 tabs project sample is using bottom navigation. To set top navigation, just change your bootstrap (in your **app.ts**) code by :

```
ionicBootstrap(MyApp,[],{tabsPlacement: "top"});
```

##Tab icon
[Back to top](#ionic-2)  

Customize tab icon

It's pretty easy to do actually. When you set a tabIcon property, Ionic sets a class name on the tab, based on the name you provided. So for example, if you set ```tabIcon="customicon"```, then the resulting class names will be ```.ion-ios-hygglo-customicon``` and ```.ion-ios-hygglo-customicon-outline``` (for selected tabs) for iOS. On Android, the prefix will be ```.ion-md-``` instead of ```.ion-ios-```.

Then just create a custom css, something like this:

```css
.ion-ios-customicon,
.ion-md-customicon {
  content: url(../../assets/img/ui/customicon.svg);
  width: 24px;
  height: 32px;
  padding: 6px 4px 2px;
  opacity: 0.9;
}
```


##Alert dialog box
[Back to top](#ionic-2)  

Here's a sample code to show a confirmation dialog box. The key is to add Alert import and then, don't miss to add alert object to current navigation stack

```javascript
import {Component, NavController, Alert} from 'ionic-angular';
import {Data} from '../../providers/data/data';

@Component({
  templateUrl: 'build/pages/home/home.html'
})
export class HomePage {

  static get parameters(){
    return [[Data], [NavController]];
  }
  //Chargement de la base de données
  constructor(dataService, nav) {
    this.dataService = dataService;
    this.items = [];
    this.nav = nav;
  }
  
  doAlert(item){
  	let confirm = Alert.create({
          title: "Suppression",
          message: 'Êtes-vous certain de vouloir supprimer l\'item ' + item.message + ' ?',
          buttons: [
            {
              text: 'Non',
              handler: () => {
                console.log('Disagree clicked');
              }
            },
            {
              text: 'Oui',
              handler: () => {
                this.dataService.deleteDocument(item);            
              }
            }
          ]
        });
      
      this.nav.present(confirm);
  }
}
```

##Floating button
[Back to top](#ionic-2) 

This snippet show how to fix floating button in front of a list

```xml
<ion-content padding class="page1">
  <ion-list>
    <ion-item *ngFor="let item of items">
      ...
    </ion-item>
  </ion-list>
</ion-content>
<button fab fab-bottom fab-right fab-fixed style="z-index:100">
  <ion-icon name="add"></ion-icon>
</button>
```

##chart
[Back to top](#ionic-2) 

[link : ng2-chart](http://valor-software.com/ng2-charts/)    
[forum : related post](https://forum.ionicframework.com/t/solved-ionic-2-ng2-charts/42926)    

##grid
[Back to top](#ionic-2) 


[link : complex layout using grid and flexbox](http://www.joshmorony.com/an-in-depth-look-at-the-grid-system-in-ionic-2/) 

##toggle
[Back to top](#ionic-2) 

####View.html

```xml
...
<ion-content padding>
  <ion-item>
    <ion-label>Tracking</ion-label>
    <ion-toggle id="trackingButton" black checked="false" (ionChange)="refreshTracking($event)"></ion-toggle>
  </ion-item>
</ion-content>
```

####View.ts

```javascript
refreshTracking(e){
   console.log("refreshTracking " + e.checked);
}
```

##Popover menu
[Back to top](#ionic-2) 

Here is a personnal code to create popover menu like Evernote edit menu 

![alt tag](https://github.com/gsoulie/ionic/blob/master/popover_menu.png)

**View file**
```xml
<ion-content class="menucl" padding>
<ion-grid class="grid" (click)="close()">
  <ion-row>
    <ion-col style="height:70px">
      <button fab fab-left class="btn"><ion-icon name="add"></ion-icon></button>
    </ion-col>
  </ion-row>
  <ion-row>
    <ion-col style="height:70px">
      <button fab fab-left class="btn"><ion-icon name="create"></ion-icon></button>
    </ion-col>
  </ion-row>
  <ion-row>
    <ion-col style="height:70px">
      <button fab fab-left class="btn"><ion-icon name="trash"></ion-icon></button>
    </ion-col>
  </ion-row>
  <ion-row>
    <ion-col style="height:70px">
      <button fab fab-left class="btn"><ion-icon name="bookmarks"></ion-icon></button>
    </ion-col>
  </ion-row>
</ion-grid>
</ion-content>

```

**Controller file**
```javascript
import { Component } from '@angular/core';
import { NavController,ViewController } from 'ionic-angular';

@Component({
  templateUrl: 'build/pages/menu/menu.html',
})
export class MenuPage {

  constructor(private navCtrl: NavController, private viewCtrl: ViewController) {}
  close(){this.viewCtrl.dismiss();}
}

```

**Style file**
```css
.menucl {
    background-color: transparent;
}
.grid {
    padding-top:50px;
    background-color: rgba(255,255,255,0.7);
}
.rowBtn {
    height: 70px;
}
```

##Dynamic style
[Back to top](#ionic-2) 

You can dynamically change the UI component style with condition like below :

```xml
<button [style.backgroundColor]="enable ? '#00CC00' : '#FF0000'">Test</button>
```

#Known issues
[Back to top](#ionic-2) 

**Click in list item in simulator sometimes(!) doesn’t work on device**

Sometimes,  on the emulator or on device, 2 out of 3 clicks it doesn't fire the click function. To solve the issue, change ```<ion-item>``` to ```<button>``` with the styling of ```ion-item```.

```xml
<ion-list>
	<button ion-item *ngFor="let audience of audience" (click)="pushProfilesList(audience)">
		<h2 class="list-title">{{audience.segment}}</h2>
		<span class="list-info">{{audience.amount}}</span>
	</button>
</ion-list>
```


#Using image
[Back to top](#ionic-2) 

To use image in your app, create a **img** folder in your **www** folder and use **img** tag like below

**View file**
```xml
<img class="thb" src="{{item.image}}" item-left/>
```

**Controller file**

```javascript
let item = {name:"my item", image:"img/my_image.png"}
```
**IMPORTANT** don't put "**/**" before *img*

**Style file**

```css
.thb{
  width: 50px;
}
```

#Backends
##Strongloop
[Back to top](#ionic-2) 

[link : Strongloop and bluemix](http://www.raymondcamden.com/2015/10/29/strongloop-ionic-and-ibm-bluemix/)    

###Network app sample

[link : ionic 2 oauth social with firebase](http://www.gajotres.net/ionic-2-succesfull-oauth-social-login-with-firebase/)
[link : ionic framework and firebase](https://www.toptal.com/front-end/building-multi-platform-real-time-mobile-applications-using-ionic-framework-and-firebase)

**cordova plugin installation**

```
cordova plugin add cordova-plugin-whitelist
cordova plugin add cordova-plugin-inappbrowser@1.1.0
```

**app.html configuration**

```html
<meta http-equiv="Content-Security-Policy" content="default-src *; script-src 'self' 'unsafe-inline' 'unsafe-eval' *; style-src  'self' 'unsafe-inline' *">
```

##Firebase
[Back to top](#ionic-2) 

###Install firebase

```
$ npm install angularfire2 --save-dev
$ npm install firebase --save-dev

$ typings install angularfire2 --save --global
$ typings install firebase --save --global
```

###Create application on Firebase

The first step consist to create your application (web application type) on the Firebase dashboard. Next, you can go to **Database** section and upload your data with JSON file like : 

```javascript
{
	"site": [{
		"id": "1",
		"libelle": "Paris"
		},{
		"id": "2",
		"libelle": "London"
		}
	],
	"user": [{
		"id": "1",
		"nom": "Jean DUPONT"
		},{
		"id": "2",
		"nom": "Martin DURAND"
		}
	],
	"type": [{"id":"1", "libelle":"Smartphone Android"},
		{"id":"2", "libelle":"Tablette Android"},
		{"id":"3", "libelle":"iPhone"}
	]
}
```

###Retrieve data inside controller

```javascript
constructor(){
	this.baseRef = new Firebase('https://project-<your_fireapp_id>.firebaseio.com/');
	this.getData();
}

getData(){
	this.baseRef.on("value", 
      	(snapshot) => {
        	let dataSet = snapshot.val();
        	this.sites =  dataSet.site || [];
        	this.users = dataSet.user || [];
        	this.devicesList = dataSet.type || [];
      },
      (error) => {
        console.log("ERREUR de récupération des données : " + JSON.stringify(error));
      });
}
```


###Retrieve data with Provider

**TODO** : To verify

For retrieving data, first create a provider (``ìonic g provider FirebaseService```) to give access to your firebase with :

```javascript
import {Injectable} from '@angular/core';
import {Observable} from 'rxjs/Observable';
import {Http} from '@angular/http';
import 'rxjs/add/operator/map';

@Injectable()
export class FirebaseService {
  baseRef = new Firebase('https://project-<your_app_id>.firebaseio.com/');
  constructor(public http: Http) {
    // check for changes in auth status
        /*this.baseRef.onAuth((authData) => {
            if (authData) {
                console.log("User " + authData.uid + " is logged in with " + authData.provider);
            } else {
                console.log("User is logged out");
            }
        })*/
  }
  getData(_tableName, _callback){
    //console.log("PROVIDER - getData : " + _tableName);
    let res;
    this.baseRef.on("value", 
      (snapshot) => {
        let dataSet = snapshot.val();
        //console.log("PROVIDER - resultset : " + JSON.stringify(dataSet));
        switch(_tableName){
          case "site": 
            res =  dataSet.site || [];
            break;
          case "users": 
            res = dataSet.user || [];
            break;
          case "type": 
            res = dataSet.type || [];
            break;
          default : 
            res =  dataSet || [];
            break;
        }
        
        if(_callback){_callback(res);}
    },
    (error) => {
      console.log("ERREUR de récupération des données : " + JSON.stringify(error));
    });
  }
}
```

Then, in your home page, add your provider like below :

```javascript
import {FirebaseService} from '../../providers/firebase-service/firebase-service';

@Component({
  templateUrl: 'build/pages/page1/page1.html',
  providers: [FirebaseService]
})

export class HomePage {
  public items: any[];
  
  constructor(public nav: NavController, public navParams: NavParams, public fb: FirebaseService) {
    fb.getData("type", function(e){
	  console.log("callback return : " + JSON.stringify(e));
	  t = e;
	});
  }
}
```

#Internationalization
[Back to top](#ionic-2)  

**cordova plugin installation**

```
$ cordova plugin add cordova-plugin-whitelist
```

**configure index.html**

```html
<meta http-equiv="Content-Security-Policy" content="default-src *; script-src 'self' 'unsafe-inline' 'unsafe-eval' *; style-src  'self' 'unsafe-inline' *">
```

**Intallation of NG2-Translate**

```
$ npm install ng2-translate --save
```

**Create each langage i18n file**

First, create **assets** folder under **www**, next jum into **assets** and create **i18n** folder.

Create as many json files whose names are equal to a specific locale/language name. For example, we will work with en, de and fr locals, so our file structure should look like this:

```
www/assets/i18n:en.json
www/assets/i18n:de.json
www/assets/i18n:fr.json
```

Each i18n file looks like :

```javascript
{
    "title" : "Internationalization Example",   
    "segment": {    
        "puppies": "Puppies",
        "kittens": "Kittens"
    }
}
```

**Import ng2-translate into app.js**

```javascript
import {Platform} from 'ionic/ionic';
import {Component} from '@angular/core';
import {HomePage} from './pages/home/home';
import {TranslateService, TranslatePipe} from 'ng2-translate/ng2-translate';
 
 
@Component({
  template: '<ion-nav [root]="rootPage"></ion-nav>',
  config: {},
  providers: [TranslateService],
  pipes: [TranslatePipe]
})
 
export class MyApp {
  constructor(platform: Platform, translate: TranslateService,) {
    this.rootPage = HomePage;
    this.translate = translate;    
 
    this.initializeTranslateServiceConfig();
  }
 
  initializeTranslateServiceConfig() {
    var prefix = 'assets/i18n/';
    var suffix = '.json';
    this.translate.useStaticFilesLoader(prefix, suffix);
 
    var userLang = navigator.language.split('-')[0];
    userLang = /(de|en|hr)/gi.test(userLang) ? userLang : 'en';
 
    this.translate.setDefaultLang('en');
 
    this.translate.use(userLang);
  }
}
```

**configure ng2-translate service**

```javascript
initializeTranslateServiceConfig() {
  var prefix = 'assets/i18n/';
  var suffix = '.json';
  this.translate.useStaticFilesLoader(prefix, suffix);
 
  var userLang = navigator.language.split('-')[0];
  userLang = /(de|en|hr)/gi.test(userLang) ? userLang : 'en';
 
  this.translate.setDefaultLang('en');
 
  this.translate.use(userLang);
}
```

For this code to work we need to find current navigator language. If current language is one of three predefined (en, de, or hr) we will use it as an initial application language. If not, we’ll use English as a default one:

**HomePage configuration**

```javascript
import {Component} from 'ionic/ionic';
import {TranslateService, TranslatePipe} from 'ng2-translate/ng2-translate';
 
@Component({
  templateUrl: 'build/pages/home/home.html',
  pipes: [TranslatePipe]
})
export class HomePage {
  constructor(translate: TranslateService) {
    this.translate = translate;
    this.pet = 'puppies';
  }
}
```

**HomePage view**

```xml
<ion-navbar *navbar>
  <ion-title>
    {{ "title" | translate }}
  </ion-title>
</ion-navbar>
 
<ion-content class="home">
  <div padding>
    <ion-segment [(ngModel)]="pet">
      <ion-segment-button value="puppies">
        {{ "segment.puppies" | translate }}
      </ion-segment-button>
      <ion-segment-button value="kittens">
        {{ "segment.kittens" | translate }} 
      </ion-segment-button>      
    </ion-segment>
  </div>
 
  <div [ngSwitch]="pet">
    <ion-list *ngSwitchWhen="'puppies'">
      <ion-item>
        <ion-thumbnail item-left>
          <img src="http://ionicframework.com/dist/preview-app/www/img/thumbnail-puppy-1.jpg">
        </ion-thumbnail>
        <h2>Ruby</h2>
      </ion-item>
    </ion-list>
 
    <ion-list *ngSwitchWhen="'kittens'">
      <ion-item>
        <ion-thumbnail item-left>
          <img src="http://ionicframework.com/dist/preview-app/www/img/thumbnail-kitten-3.jpg">
        </ion-thumbnail>
        <h2>Luna</h2>
      </ion-item>
    </ion-list>
  </div>
</ion-content>
```

#Splash screen and appicon
[Back to top](#ionic-2)

[link : Appicon and Splash screen documentation](http://blog.ionic.io/automating-icons-and-splash-screens/)

[link : Splash screen PSD](http://code.ionicframework.com/resources/splash.psd)

Save a splash.png, splash.psd or splash.ai file within the resources directory at the root of the Cordova project. Splash screen dimensions vary for each platform, device and orientation, so a square source image is required the generate each of various sizes. The source image’s minimum dimensions should be 2208x2208 px, and its artwork should be centered within the square, knowing that each generated image will be center cropped into landscape and portrait images. The splash screen’s artwork should roughly fit within a center square (1200x1200 px). This Photoshop splash screen template provides the recommended size and guidelines of the artwork’s safe zone. Additionally, when the Orientation preference config is set to either landscape or portrait mode, then only the necessary images will be generated.

For the appicon, the minimum dimension should be 192x192 px with no rounded corner. 1024x1024 px file is better 

```
$ ionic resources --splash
```

You can also run 

```
$ ionic resources --icon
```

Or simply

```
$ ionic resources
```

**Note :** If splash screen doesn't showing, update your cordova plugin

```
ionic plugin rm cordova-plugin-splashscreen
ionic plugin add https://github.com/apache/cordova-plugin-splashscreen.git
```

**Remove fade-in / fade-out effect**

Add the following property to config.xml
```xml
<preference name="FadeSplashScreen" value="false"/>
```

**Remove spinner**
Add the following property to config.xml
```xml
<preference name="ShowSplashScreenSpinner" value="false"/>
```

#Beta testing
[Back to top](#ionic-2)

Available for iOS and Android, Ionic View makes it easy to **test** and **share** your app directly **on the device**. **A developer, client, customer, or friend** can download Ionic View, enter the App Id for your app, and immediately load and test the app. With hundreds of thousands of installs, Ionic View is becoming a core part of the Ionic development experience.

[link : Ionic View](http://blog.ionic.io/rapid-development-with-ionic-view/)


#Push notification
[Back to top](#ionic-2) 

First way, using push notification module, only works when app is opened

```javascript
this.platform.ready().then(() => {
  console.log('Platform ready');
  this.initPush();
}

initPush() {
  let push = Push.init({
      android: {
          senderID: "XXXXXX"
      },
      ios: {
          alert: "true",
          badge: true,
          sound: 'false'
      },
      windows: {}
  });

  push.on('registration', (data) => {
      console.log("REGISTRATION");
          localStorage.setItem('token', data.registrationId);
  });

  push.on('notification', (data) => {
      console.log("ONLY WORK'S WHEN APP IS OPEN")
  });

  push.on('error', (e) => {
      console.log(e.message);
  });
```

Using push notification when app is closed needed to use background service because ionic is a web application, so the javascipt file will only be triggered/fired when the application is opened.

**TODO** using ionic.io

[push notification ionic 2](http://ionicframework.com/docs/v2/native/Push/)    

- plugins installation
```
$ ionic add ionic-platform-web-client
$ ionic plugin add phonegap-plugin-push
$ ionic io init
$ ionic config set dev_push true
```

- in ```webpack.config.js``` Add the following line :

```
module.exports = {
  entry: [
    path.resolve('bower_components/ionic-platform-web-client/dist/ionic.io.bundle'),
    ......
```

- in ```bower_components/ionic-platform-web-client/dist/ionic.io.bundle.js``` replace:

```"IONIC_SETTINGS_STRING_START";"IONIC_SETTINGS_STRING_END";``` with :

```javascript
  "IONIC_SETTINGS_STRING_START";
    var settings = {
            "app_id": "YOUR APP_ID",
            "api_key": "YOUR APP_KEY",
            "gcm_key": "YOUR GCM_KEY",
            "dev_push": true
        };
        
    return {
        get: function(setting) {
            if (settings[setting]) {
                return settings[setting];
            }
            return null;
        }
    };
  "IONIC_SETTINGS_STRING_END";
``` 

- Lastly, in your index.html you can remove ```<script src="lib/ionic-platform-web-client/dist/ionic.io.bundle.min.js"></script>``` but leave ```<script src="cordova.js"></script>``` commented out.

- Everything should work now. To initiate the push service, use:

```javascript
    Ionic.io();
    ionicPush = new Ionic.Push().init({
        debug: true,
        onNotification: (data) => {
            console.log('New push notification received');
            console.log(data);
        }
    });

    ionicPush.register(data => {
        console.log("Device token:", data.token);
    });
```

#Publishing app
[Back to top](#ionic-2)

[link : publishing app](http://ionicframework.com/docs/guide/publishing.html)    

###Enable prodMode

To enable prod mode, I configured the following in app.ts:

```javascript
import {enableProdMode} from '@angular/core';
enableProdMode();
```

or other solution

```javascript
let prodMode: boolean = window.hasOwnProperty('cordova');
```

Now that we have a working app, we are ready to push it live to the world! Since the Ionic team already submitted the Todo app from this guide to the app store, chances are you’ll want to follow this chapter with a new app that you make on your own.

So first, we need to generate a release build of our app, targeted at each platform we wish to deploy on. Before we deploy, we should take care to adjust plugins needed during development that should not be in production mode. For example, we probably don’t want the debug console plugin enabled, so we should remove it before generating the release builds:

```
$ cordova plugin rm cordova-plugin-console
```

##Android publishing

First, check your config.xml file located in :

```
app/platforms/ios/AppName/config.xml
app/platforms/android/res/xml
```

more information about it's configuration [here](http://cordova.apache.org/docs/en/latest/config_ref/index.html)

To generate a release build for Android :

```
$ cordova build --release android
```

This will generate a release build based on the settings in your config.xml. Your Ionic app will have preset default values in this file, but if you need to customize how your app is built, you can edit this file to fit your preferences

Next, we can find our unsigned **APK** file in ```platforms/android/build/outputs/apk```

Now, we need to sign the unsigned APK and run an alignment utility on it to optimize it and prepare it for the app store. If you already have a signing key, skip these steps and use that one instead.

Let’s generate our private key using the **keytool** command that comes with the JDK.

```
$ keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
```

You’ll first be prompted to create a password for the keystore. Then, answer the rest of the nice tools’s questions and when it’s all done, you should have a file called **my-release-key.keystore** created in the current directory.

**Note:** Make sure to save this file somewhere safe, if you lose it you won’t be able to submit updates to your app!

To sign the unsigned APK, run the **jarsigner** tool which is also included in the JDK:

```
$ jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore HelloWorld-release-unsigned.apk alias_name
```

This signs the apk in place. Finally, we need to run the zip align tool to optimize the APK. The **zipalign** tool can be found in **/path/to/Android/sdk/build-tools/VERSION/zipalign**. For example, on OS X with Android Studio installed, **zipalign is in ~/Library/Android/sdk/build-tools/VERSION/zipalign:**

```
$ zipalign -v 4 HelloWorld-release-unsigned.apk HelloWorld.apk
```

Now we have our final release binary called HelloWorld.apk and we can release this on the Google Play Store


#TODO
[Back to top](#ionic-2)

###Testing Backand backend

[link : Backand](https://devdactic.com/ionic-backend-database/)   
[link : Backand integration](https://www.backand.com/integrations/)    

Backand is an alternative to Firebase (only NoSQL approach). The main difference is that Backand can be integrated with ohter database than NoSQL, like MySQL, PostgreSQL, MSSQL and Oracle. 
On the other hand, Backand doesn't have offline support instead of Firebase

###Testing Telerik backend

Telerik is a company with a lot of cool products (like NativeScript) which I haven’t had much of a chance to play around with yet, and they also offer a BaaS product for mobile applications. As far as a feature set goes they cover just about everything with offline support, data storage, file storage, social integration, push notifications and more.

Similar to Backand, Telerik Backend Services can also connect to any existing MSSQL, MySQL, PostgreSQL or Oracle databases. If you’re coming from Parse and want a similar set of features, Telerik Backend Services will likely be a good option for you.
