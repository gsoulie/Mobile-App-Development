![alt tag](https://github.com/gsoulie/ionic/blob/master/ionic2ban.png)

#ionic 2

> **Warning** this personnal guide is based on the beta of ionic 2. Consequently, some information may be outdated

##### Table of Contents  
* [Prerequisites](#prerequisites)    
	* [Start with ionic](#start-with-ionic)  
	* [Visual Studio Code](#visual-studio-code)    
* [Concepts](#concepts)    
	* [Angular 2](#angular-2)  
	* [Decorators](#decorators)    	
	* [Pipe](#pipe)    
	* [Promise vs Observable](#promise-vs-observable)    
	* [Mapping](#mapping)    
	* [Arrow function](#arrow-function)    
* [Directives](#directive)    
* [Config](#config)    
* [Global variables](#global-variables)    
* [Add files to project](#add-files-to-project)    
* [Third party lib](#third-party-lib)    
* [Useful functions](#useful-functions)  
	* [Get specific platform](#get-specific-platform)   
	* [Generate UUID](#generate-uuid)    
	* [Show / hide DOM element](#show-hide-dom-element)    
	* [Checking network connection](#checking-network-connection)    
	* [Close modal](#close-modal)    
* [Moment JS](#momentjs)    
* [File storage](#file-storage)  
* [Geolocation](#geolocation)  
* [Database](#database)  
	* [SQLite database](#sqlite-database)    
	* [SQLStorage](#sqlstorage)    
* [Camera](#camera)   
* [Gallery](#gallery)    
* [Barcode Scanner](#barcode-scanner)  
* [HTTP Remote and Local data](#http-query)  
* [Navigation](#navigation)  
* [Themes](#themes)  
* [Events](#events)    
	* [Page event](#page-event)    
	* [Event propagation](#event-propagation)    
* [UI Components](#ui-components)    
	* [modal](#modal)    
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
	* [popover menu](#popover-menu)    
	* [dynamic style](#dynamic-style)    
	* [Toggle menu](#toggle-menu)    
* [Sass](#sass)    	
* [Known issues](#known-issues)    
* [Using image](#using-image)    
* [Forms](#forms)    
* [Backends](#backends)    
	* [Strongloop](#strongloop)     
	* [Firebase](#firebase)     
* [Authentication](#authentication)    
* [Internationalization](#internationalization)  
* [Splash screen and appicon](#splash-screen-and-appicon)  
* [Beta testing](#beta-testing)    
* [Push notification](#push-notification)   
* [Build for iOS](#build-for-ios)    
* [Publishing App](#publishing-app)  
* [Other modules](#other-modules)    
* [Self working components](https://github.com/gsoulie/Ionic2-snippets)    

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
$ sudo npm install -g ionic
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

**Generate new provider in ionic 2 project**

It creates new folder in the project treeview

```
$ ionic g provider myProvider
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

##Visual Studio Code
[Back to top](#ionic-2) 

Another very good alternative to Atom is [visual studio code] (https://code.visualstudio.com/c?utm_expid=101350005-27.GqBWbOBuSRqlazQC_nNSRg.2&utm_referrer=https%3A%2F%2Fwww.google.fr%2F)

###Some useful extensions

* [Ionic2 extension](https://marketplace.visualstudio.com/items?itemName=Thavarajan.ionic2)    
* [Auto Import extension](https://marketplace.visualstudio.com/items?itemName=steoates.autoimport)    
* [Angular 2 - TypeScript snippets](https://marketplace.visualstudio.com/items?itemName=johnpapa.Angular2)    
* [Git History] (https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)    
* [custom icons theme](https://code.visualstudio.com/blogs/2016/09/08/icon-themes)    
* [npm intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.npm-intellisense)    
* [sass lint](https://marketplace.visualstudio.com/items?itemName=glen-84.sass-lint)    
* [TSlint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)    

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
<button ion-button (click)="someFunction($event)">
```

This will call the someFunction function and pass in the event whenever the button is clicked on. You can replace click with any native or custom event you like. You can also use the following syntax:

```xml
<button ion-button (^click)="someFunction($event)">
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
<button ion-button (click)="myParagraph.innerHTML = 'Once upon a time...'">
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

*View file*

Pipe inline syntax : ```value | myPipe:args[0]:args[1]```

```xml
<ion-label>{{name | helloWorld}}</ion-label>
```

> Note: The first letter of the pipe's name in the view file is in lower case

###Other example

*Pipe file*

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

*Page file*

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

*View file*

```
The meaning of life: {{mySingleInt | addInt:2}}

<ul>
<li *ngFor="let myInt of myIntArray">
{{myInt | addInt:1}}
</li>
</ul>
```


###Other example Date format pipe

*Pipe file* (app/pipe/datePipe.js)

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

*Controller file*

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

*View file*

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

*Example :* using Promise or Observable

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


##Arrow function
[Back to top](#ionic-2) 

[link : official documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

[link : other useful doc](https://basarat.gitbooks.io/typescript/content/docs/arrow-functions.html)

*definition* : An arrow function expression has a shorter syntax compared to function expressions and does not bind its own this, arguments, super, or new.target. Arrow functions are always anonymous. These function expressions are best suited for non-method functions and they can not be used as constructors.

*summarize* : 

- You don't need to keep typing function
- It lexically captures the meaning of **this**
- It lexically captures the meaning of arguments

*notation* :  

```javascript
() => {/*statement*/}

//With parameters
(param1, param2,...) => {/*statement*/}
```

###Usage

this has traditionally been a pain point in JavaScript. Fat arrows fix it by capturing the meaning of this from the surrounding context. So it is very useful in case of calling asynchronous callback after a window closing event.

use case : 

We want to refresh a list item window after adding a new item (via a "new item" modal)

*List.ts*

```javascript
...

// Refresh item list
refreshRouteList(){
	this.Db.getRoutesList().then((data)=> this.routesList = data);
}

//Open new item modal
newItem(){
	this.navCtrl.push(DetailPage,{callback:
		() => {this.refreshRouteList();}
	});
 }
 
 ...
```


*DetailPage.ts*

```javascript
...
ionViewDidLeave(){
	console.log("close page");
	this.callback();
}
...
```

#Directive
[Back to top](#ionic-2)  

###ngFor

To declare more than one variable in ngFor directive, use :

```xml
<ion-badge *ngFor="let cat of category; let i=index">...</ion-badge>
```


#Config
[Back to top](#ionic-2)  

The Config lets you configure your entire app or specific platforms. You can set the tab placement, icon mode, animations, and more for each platform. 

[link : Config official documentation](http://ionicframework.com/docs/v2/api/config/Config/)

*app.module.ts*

```javascript
import { IonicApp, IonicModule } from 'ionic-angular';

@NgModule({
  declarations: [ MyApp ],
  imports: [
    IonicModule.forRoot(MyApp, {
      backButtonText: 'Go Back',
      iconMode: 'ios',
      modalEnter: 'modal-slide-in',
      modalLeave: 'modal-slide-out',
      tabsPlacement: 'bottom',
      pageTransition: 'ios'
    }, {}
  )],
  bootstrap: [IonicApp],
  entryComponents: [ MyApp ],
  providers: []
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
#Add files to project
[Back to top](#ionic-2)

Since RC0, all the files you need to add in your project (like json file, image etc...) must be added in **YOUR_APP/src/assests/data.**

#Third party lib
[Back to top](#ionic-2)

##ES6
To use a custom lib file in your project, follow the next steps 

###1 Create "lib" folder under app

```
/app/lib/utils.js
```

###2 implement lib file

*utils.js*
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

*From Home.js*
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

*utils.ts*
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
```
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

//Get environment variable with process.env.IONIC_ENV
if (process.env.IONIC_ENV == 'prod') {
  // production mode
  
} else {
  // dev mode 'dev'
}

-->
/*
window.addEventListener("orientationchange", function() {
    alert(window.orientation);
}, false);*/

ionic.Platform.exitApp(); // stops the app
```
 
##Generate UUID
[Back to top](#ionic-2) 

To simply generate UUID like "547d8e40-354c-11e6-aa97-083e8ec535fb"

```javascript
import { UUID } from 'angular2-uuid';
let uuid = UUID.UUID();
```

##Show hide DOM element
[Back to top](#ionic-2) 

####Solution 1

Consider that we have a card with a quote wich can be add/remove to favorites. We only show one of the two button : "add to favorites" when the quote is not in the favorites list, and "remove from favorites" when the quote is already in the favorites list. To do this, we will use a *ngIf* directive.

*View file*

```xml
...
<button ion-button (click)="addToFavorites" *ngIf="!isFavorite(quote)">Add to favorite</button>
<button ion-button (click)="removeFromFavorites" *ngIf="isFavorite(quote)">Remove from favorite</button>
...
```

*Controller file*
```javascript
export class HomePage {
	...
	isFavorite(quote: Quote){
		return this.myService.isQuoteFavorite(quote);
	}
	
	// Add the quote to the favorites list
	addToFavorites(quote: Quote){ ... }

	// remove the quote from the favorites list
	removeFromFavorites(quote: Quote){ ... }

}
```

####Solution 2

The next solution is to use the *hidden* property of an element

```xml
<button ion-button (click)="removeNote()" [hidden]="creationMode" icon-only>
	<ion-icon name="trash"></ion-icon>
</button>
```

*controller.ts*
```javascript
export class HomePage {
  creationMode: boolean = false;
  ... 
}
```

> Angular JS 2 update : don't use hidden anymore

Prefer use this syntax

*view file*
```html
<button ion-fab fab-left icon-only [style.display]="menuIsOpen ? 'inherit':'none'">
   <ion-icon name="star"></ion-icon>
</button>
```

*controller file*
```javascript
menuIsOpen: boolean = false;
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
	
*View file*
```xml
<button ion-button (click)="close()"></button>
```

*Controller file*

Don't forget to import *ViewController*

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
import * as moment from 'moment';	//syntax for ionic beta
Import moment from 'moment'	//RC0
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


#File storage
[Back to top](#ionic-2)  

[File Documentation here](https://ionicframework.com/docs/v2/native/file/)    

First install the plugin :

```
$ ionic plugin add cordova-plugin-file
```

Next let see an example of photo storage in a new file

*Controller file*

```javascipt
import { ModalController } from "ionic-angular";
import { Camera, File, Entry, FileError } from "ionic-native";

/**************************** 
 * IMPORTANT
 ***************************/
declare var cordova: any;	// trick wich inform typescript that this cordova variable will available at the runtime

export class HomePage {
    imageUrl = '';

    constructor(private modalCtrl: ModalController) {}

    onTakePhoto() {
        // See the documentation for more camera options
        Camera.getPicture({
            encodingType: Camera.EncodingType.JPEG,
            correctOrientation: true
        })
        .then(
            imageData => {
	    	// Save image to File
		const currentName = imageData.replace(/^.*[\\\/]/, '');	// extract the image name
		const path = imageData.replace(/[^\/]*$/, '');	// extract the image path
		const newFileName = new Date().getUTCMilliseconds() + ".jpg";
		File.moveFile(path, currentName, cordova.file.dataDirectory, newFileName)	// warning on cordova variable
		.then(
			(data: Entry) => {
				this.imageUrl = data.nativeURL;
				Camera.cleanup();
			}
		)
		.catch(
			(err: FileError) => {
			this.imageUrl = '';
			Camera.cleanup();
		});
                this.imageUrl = imageData;
            }
        )
        .catch(
            err => {console.log(err);}
        );
    }
    
    removeFile(place: Place){
	const currentName = place.imageUrl.replace(/^.*[\\\/]/, '');	// extract the image name
	File.removeFile(cordova.file.dataDirectory, currentName)
	.then(
		() => console.log("removed");
	)
	.catch(
		() => {
			console.log("error");
		}
	);
    }
}
```

#Geolocation
[Back to top](#ionic-2)  

[link : google map geolocation](http://www.joshmorony.com/ionic-2-how-to-use-google-maps-geolocation-video-tutorial/)

###Angular2 Google maps integration

First we are going to see how to add a map on our application and add / display markers

So, first install angular2-google-maps package :

```
npm install --save angular2-google-maps
```

Then insert the *sebm-google-map* module to your view file

*View file (SetLocationPage.html)*

```xml
<ion-content>
	<sebm-google-map 
	[latitude]="location.lat" 
	[longitude]="location.lng" 
	[zoom]="16"
	(mapClick)="onSetMarker($event)">
		<sebm-google-map-marker [latitude]="marker.lat" [longitude]="marker.lng" *ngIf="marker"></sebm-google-map-marker>
	</sebm-google-map>
	<button ion-button block (click)="onConfirm()" [disabled]="!marker">Confirm</button>
</ion-content>
```
Next, add the module dependency in your *app.module.ts* file

Note that you first need to get a google map Api key 

[see angular-maps setup](https://angular-maps.com/docs/getting-started.html)    
[Get your GMAP API Key](https://developers.google.com/maps/documentation/javascript/get-api-key?hl=en#key)    

**GMAP API KEY summary**

1 - [Get your GMAP API Key here](https://developers.google.com/maps/documentation/javascript/get-api-key?hl=en#key)    
2 - Click on the *GET A KEY* button     
3 - Select your firebase project in the list or create a new    
4 - Copy the generated key    
5 - Insert the key in your AgmCoreModule configuration (like below)    

*app.module.ts*

```javascript
...
import { AgmCoreModule } from "angular2-google-maps/core";

@NgModule({
	declarations : [...],
	imports: [
		...,
		AgmCoreModule.forRoot({
			apiKey: 'qsodkpazd51a6dz5a65z1eq24drsd5sd'
		})
	],
	...
})

```

Next you must specify a height in your scss file else your view will be empty :

*Style file (SetLocationPage.scss)*
```css
page-set-location-page {
	sebm-google-map {
		height: 250px;
	}
}
```

*Controller file (SetLocationPage.ts)*

```javascript
import { NavParams, ViewController } from "ionic-angular";

export class LocationPage {
	location: any = {};	// Note : can be an object of class "Location" containing lat and lng attributes
	marker: any = {};
	
	constructor(private navParams: NavParams, private viewCtrl: ViewController) { 
		this.location = this.navParams.get("location"); 
		
		// retrieve chosen marker
		if(this.navParams.get('isSet')) {
			this.marker = this.location;
		}
	}

	// Add marker on the map
	onSetMarker(event: any){
		this.marker = {lat: event.coords.lat, lng: event.coords.lng};
	}
	
	// Confirm the location and pass the chosen location back to the page
	onConfirm(){
		// Close the modal with the chosen location
		this.viewCtrl.dismiss({location: this.marker});
	}
	
}
```

Finally, call your Location page :

*Controller file (addPlace.ts)*

```javascript

import { SetLocationPage } from "../set-location/set-location";

export class LocationPage {
	// Note : can be an object of class "Location" containing lat and lng attributes
	location: any= {
	    lat: 40.7624324,
	    lng: -73.9759827
	};
	locationIsSet = false;
	
	constructor(private modalCtrl: ModalController) {}
	
	// open map modal which permit to choose a position and get back chosen location
	onOpenMap() {
		const modal = this.modalCtrl.create(SetLocationPage, 
		{location: this.location, isSet: this.locationIsSet});
		modal.present();
		modal.onDismiss(data => {
			if(data){
				this.location = data.location;
				this.locationIsSet = true;
			}
		});
	}
	
	// Locate the current position 
	onLocate() {
		
	}
}
```


*View file (addPlace.html)*

```xml
<ion-content>
    <form #f="ngForm" (ngSubmit)="onSubmit(f)">
        <ion-list>
            <ion-item>
                <ion-label fixed>Title</ion-label>
                <ion-input type="text" name="title" ngModel required></ion-input>
            </ion-item>
            <ion-item>
                <ion-label floating>Description</ion-label>
                <ion-textarea name="description" ngModel required></ion-textarea>
            </ion-item>
        </ion-list>
        <ion-grid>
            <ion-row>
                <ion-col>
                    <button ion-button block outline type="button" (click)="onLocate()">Locate me</button>
                </ion-col>
                <ion-col>
                    <button ion-button block outline type="button" (click)="onOpenMap()">Select on map</button>
                </ion-col>
            </ion-row>
            <ion-row *ngIf="locationIsSet">
                <ion-col>
			<sebm-google-map [latitude]="location.lat" [longitude]="location.lng" [zoom]="16">
				<sebm-google-map-marker 
				[latitude]="location.lat" 
				[longitude]="location.lng">
				</sebm-google-map-marker>
			</sebm-google-map>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col text-center>
                    <h5>Take a photo</h5>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
                    <button ion-button block outline type="button" (click)="onTakePhoto()">Take a photo</button>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
        <img [src]=""></img>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
                    <button ion-button color="secondary" block type="submit" 
		    [disabled]="!f.valid || !locationIsSet">Add this place</button>
                </ion-col>
            </ion-row>
        </ion-grid>        
    </form>
</ion-content>
```

*Style file (addPlace.scss)*
```css
page-add-place {
	sebm-google-map {
		height: 250px;
	}
}
```

[Back to top](#ionic-2) 

###Using native geolocation plugin

Now we have integrated a map on our application, we will use the native geolocation plugin to locate our current position and display it on the previous map.

So, first install cordova plugin :

```
$ ionic plugin add cordova-plugin-geolocation
```

Then implement the *onLocate* function and add the import of *Geolocation* plugin. Note that we also add loading and toast components for more cool stuff.

*Controller file (addPlace.ts)*

```javascript

import { SetLocationPage } from "../set-location/set-location";
import { ModalController, LoadingController, ToastController } from "ionic-angular";
import { Geolocation } from "ionic-native";

export class LocationPage {
	// Note : can be an object of class "Location" containing lat and lng attributes
	location: any= {
	    lat: 40.7624324,
	    lng: -73.9759827
	};
	locationIsSet = false;
	
	constructor(private modalCtrl: ModalController, 
	private loadingCtrl: LoadingController, private toastCtrl: ToastController) {}
	
	// open map modal which permit to choose a position and get back chosen location
	onOpenMap() {
		...
	}
	
	// Locate the current position with native geolocation plugin
	onLocate() {
		// Initialize loader component
		const loader = this.loadingCtrl.create({
			content: 'Getting your location...'
		});
		loader.present();
		
		// Get the current position
		Geolocation.getCurrentPosition()
		.then(
			location => {
				loader.dismiss();
				this.location.lat = location.coords.latitude;
				this.location.lng = location.coords.longitude;
				this.locationIsSet = true;
			}
		)
		.catch(
			error => {
				console.log(error);
				loader.dismiss();
				const toast = this.toastCtrl.create({
					message: 'Could not get location, please pick it manually',
					duration: 2500
				});
				toast.present();
			}
		); 
	}
}
```


#Database

##SQLite database
[Back to top](#ionic-2)  

###Storage method

Storage is an easy way to store key/value pairs and JSON objects.

[documentation here](https://ionicframework.com/docs/v2/storage/)    

*Service file*

```javascript
import { Storage } from "@ionic/storage";
import { Injectable } from "@angular/core";
import { Place } from "../models/place";
import { Location } from "../models/location";

@Injectable()   // IMPORTANT
export class PlacesServices {
    private places: Place[] = [];

    constructor(private storage: Storage) {}

    addPlace(title: string, description: string, location: Location, imageUrl: string){
        const place = new Place(title, description, location, imageUrl);
        this.places.push(place);    // local storage

        this.storage.set('places', this.places)    // db storage
        .then(/* nothing specially */)
        .catch(
            err => {
                this.places.splice(this.places.indexOf(place), 1);
            }
        );
    }

    // Fetch data from DB
    fetchPlaces() {
        return this.storage.get('places')
        .then(
            (places: Place[]) => {
                this.places = places != null ? places : []; // be careful to do not return null 
		return this.places;
            }
        )
        .catch(err => console.log(err);)
    }

    loadPlaces(){
        return this.places.slice(); // Important : slice() return a copy of the object
    }

    deletePlaces(index: number){
        this.places.splice(index, 1);
	
	this.storage.set('places', this.places) // Update de data in the storage with the new places array without deleted element
	.then(
		() => {
			// doing some stuff
		}
	)
	.catch(
		err => console.log(err);
	);
    }
}
```

Next, call your fetch method

*Controller file (home.ts)*

**note** : add implementation of *OnInit*

```javascript
import { NgForm } from "@angular/forms";
import { AddPlacePage } from "../add-place/add-place";
import { Place } from "../../models/place";
import { PlacesService } from "../../providers/places";

@Component({
    selector: "page-home",
    templateUrl: "home.html"
})
export class HomePage implements OnInit{
	addPlacePage = AddPlacePage;
	places: Place [] = [];
   
	constructor() {public navCtrl: NavController, private placesService: PlacesService}

	ngOnInit() {
		this.placesService.fetchPlaces()
		.then(
			(places: Place[]) => this.places = places
		);
	}
}
```

###SQLite method

[link : Using Sqlite storage tutorial](https://devdactic.com/ionic-2-sqlstorage/)

There is two main solutions for data storage. The first one is the local HTML5 storage and the second is using SQLite database storage. HTML5 storage provide a key-value storage. This solution can be useful for small applications, but is not adapted for SQL querying. On the other hand, this solution is limitated to 10MB of data storage.

[link : using sqlite](https://www.thepolyglotdeveloper.com/2015/12/use-sqlite-in-ionic-2-instead-of-local-storage/)

This solution using the local device database. **You can make some complex SQL query** for retrieve data.

**Intallation**

After the project is created, intall cordova sqlite storage plugin

```
$ ionic plugin add cordova-sqlite-storage
```

*Database initialization (app.js)*

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

*Database manipulation (home.js)*

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
*Displaying data from database (home.html)*

```xml
<ion-header>
	<ion-navbar>
	    <ion-title>
	        Home
	    </ion-title>
	    <button ion-button clear (click)="refresh()">Refresh</button>
	    <button ion-button clear (click)="add()">Add</button>
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

[See documentation here](https://ionicframework.com/docs/v2/native/camera/)    

First install ionic-native package if needed

```
$ npm install ionic-native --save
```

Then install cordova camera plugin

```
$ ionic plugin add cordova-plugin-camera
```

Implement code

*View file (addPlace.html)*

```xml
<ion-content>
    <form #f="ngForm" (ngSubmit)="onSubmit(f)">
        <ion-list>
            <ion-item>
                <ion-label fixed>Title</ion-label>
                <ion-input type="text" name="title" ngModel required></ion-input>
            </ion-item>
            <ion-item>
                <ion-label floating>Description</ion-label>
                <ion-textarea name="description" ngModel required></ion-textarea>
            </ion-item>
        </ion-list>
        <ion-grid>
            <ion-row>
                <ion-col>
                    <button ion-button block outline type="button" (click)="onTakePhoto()">Take a photo</button>
                </ion-col>
            </ion-row>
            <ion-row *ngIf="imageUrl != ''">
                <ion-col>
		        <img [src]="imageUrl"></img>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
                    <button ion-button color="secondary" block type="submit" 
		    [disabled]="!f.valid || !locationIsSet">Add this place</button>
                </ion-col>
            </ion-row>
        </ion-grid>        
    </form>
</ion-content>
```

*Controller file (addPlace.ts)*

```javascript

import { SetLocationPage } from "../set-location/set-location";
import { ModalController } from "ionic-angular";
import { Camera } from "ionic-native";

export class LocationPage {
	imageUrl = '';

	constructor(private modalCtrl: ModalController) {}
	
	onTakePhoto() {
		// See the documentation for more camera options
		Camera.getPicture({
			encodingType: Camera.EncodingType.JPEG,
			correctOrientation: true
		})
		.then(
			imageData => {
				this.imageUrl = imageData;
			}
		)
		.catch(
			err => {
				console.log(err);
				Camera.cleanup();	// Only if the image is stored in a new File
			}
		);
	}
}
```


#Gallery
[Back to top](#ionic-2)  

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-camera
```

*import plugin in ts file*
```javascript
import { Camera } from ‘ionic-native’;
```

*declare image source component*

```javascript
private imageSrc: string;

constructor(private navCtrl: NavController) { }
```

*function to access gallery*

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

*view file*

```xml
<div class="gallery-button" text-center>
    <img [src]="imageSrc" />    
  <ion-icon name="images" on-tap="openGallery()"></ion-icon>
  <p>Choose a Photo</p>  
</div>
```

*style file*

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

**Retrieve remote data**

First, create a provider with the code below :

```javascript
import {Injectable} from '@angular/core';
import {Http} from '@angular/http';
import 'rxjs/add/operator/map';
 
@Injectable()
export class httpProvider {

  constructor(public http: Http) {
 	console.log("hello");
  }
  
  getRemoteData(){
    this.http.get('https://www.reddit.com/r/gifs/new/.json?limit=10').map(res => res.json()).subscribe(data => {
        console.log(data);
    });
  }
}
```

> Note : The **map** lib is only imported because we need is http.get function

**Usage**

In your controller, inject your provider like below :
```javascript
import {Component} from '@angular/core';
import {NavController} from 'ionic-angular';
import {httpProvider} from '../../providers/http-provider';

@Component({
    selector: 'page-home',
    templateUrl: 'home.html'
})
export class HomePage {
    constructor(public httpProvider: HttpProvider){
    }
    
    ionViewDidLoad(){
    	this.httpProvider.getRemoteData();
    }
}
```

**Retrieve local data**

As the same way, you can retrieve local data. First, create a "data" sub folder under *assets* folder which contain a *localData.json*. Then use the http with the local path

```javascript
import {Injectable} from '@angular/core';
import {Http} from '@angular/http';
import 'rxjs/add/operator/map';
 
@Injectable()
export class httpProvider {

  constructor(public http: Http) {
 	console.log("hello");
  }
  
  getRemoteData(){
    this.http.get('https://www.reddit.com/r/gifs/new/.json?limit=10').map(res => res.json()).subscribe(data => {
        console.log(data);
    });
  }
  
  getLocalData(){
    this.http.get('assets/data/localData.json').map(res => res.json()).subscribe(data => {
        console.log(data);
    });
  }
}
```


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
<button ion-button (click)="goToAbout()">About</button>
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

####Navigate using navPush directive

*View file*

```html
...
<ion-content>
	<button ion-button [navPush]="userPage">User</button>
</ion-content>
```

*Controller file*

```javascript
import { NavController } from "ionic-angular";
import { UserPage } from "../user/user";
...
export class HomePage {
	userPage = UserPage;
	
	constructor(public navCtrl: NavController) {}
}
```



#Themes
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

###Override variable.scss

In the *variable.scss* file, you can define a lot of variables to create your custom style (see more on [ionic 2 overriding variables](#https://ionicframework.com/docs/v2/theming/overriding-ionic-variables/). Here is an example of variable.scss overriding

*variable.scss*

```javascript
...
// Shared variables
$myOwnVariable: <value>;
$content-padding: 5px;

// Colors variables
$color: {
	primary: ...
	secondary: ...
	...
}

```

*note* : New colors variables must be called with ```<Button color="myNewColor">```

#UI Components

##Modal
[Back to top](#ionic-2)  

Consider that we have a page (UserListPage for example) with a button wich open a modal based on UserPage controller.

*UserListPage Controller file*

```javascript
import { ModalController } from 'ionic/angular';
...
users: User[];

constructor(private modalCtrl: ModalController){}

openMyModal(user: User){
	const modal = this.modalCtrl.create(UserPage, username);
	modal.present();
	modal.onDidDismiss((remove: boolean) => {
		//call the dismiss method of the UserPage controller
		if(remove) {
			// if remove = true then remove user from database
			this.myService.removeUser(user);

			// refresh user list : 2 methods
			// 1 - reload all the list
			this.users = this.myService.getAllUsers();
			
			// 2 - remove only deleted user from users array
			const position = this.users.findIndex((userEl: User) => {
				return userEl.id == user.id;
			});
			this.users.splice(position, 1);
			
		}
	});
}
...
```

*UserPage controller file*

```javascript
...
constructor(private viewCtrl: ViewController, private navParams: NavParams){}

ionViewDidLoad(){
	...
}

/**
 * @param{Boolean} remove : if true, remove the user from database
 */
onClose(remove = false){
	this.viewCtrl.dismiss(remove);	
}
...
```


##ComboBox
[Back to top](#ionic-2)  

*View file*
```xml
<ion-item>
	<ion-label>Profession</ion-label>
	<ion-select [(ng-model)]="prof" (ionChange)="selectObject($event)">
		<ion-option *ngFor="let item of professions" value="{{item.objectId}}">{{item.titre}}</ion-option>
	</ion-select>
</ion-item>
```

*Controller file*

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

*View file*

```xml
<ion-content padding class="page1">
  <ion-list>
    <ion-item *ngFor="let item of items" (click)="openDetail(item.idDevice, item.nom)">
      <button ion-button clear item-right (click)="pickDevice($event,item.idDevice)">
        <ion-icon green name="phone-portrait" item-right></ion-icon>
      </button>
      <h2>{{item.nom}}</h2>
    </ion-item>
  </ion-list>
</ion-content>
```

*Controller file*

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
      <button ion-button (click)="showEditModal(item, slidingItem)"><ion-icon name="create"></ion-icon>Bearbeiten</button>
      <button ion-button danger (click)="doConfirm(item, slidingItem)"><ion-icon name="trash"></ion-icon>Löschen</button>
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
        <button ion-button (click)="showEditModal(item, slidingItem)"><ion-icon name="create"></ion-icon>Bearbeiten</button>
        <button ion-button danger (click)="doConfirm(item, slidingItem)"><ion-icon name="trash"></ion-icon>Löschen</button>
      </ion-item-options>
    </ion-item-sliding>
  </template>
</ion-list>
```


###Remove item from list

*View file*

```xml
<ion-list>
    <ion-item-sliding *ngFor="let post of posts">
    	<ion-item>
    	...
    	</ion-item>
    	<ion-item-options>
    	    <button ion-button danger (click)="removePost(post)" icon-only>
    	    	<ion-icon name="remove"></ion-icon>
    	    </button>
    	</ion-item-options>
    </ion-item-sliding>
</ion-list>
```

*Controller file*

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
        <button ion-button color="darkgrey" (click)="removeNote(item)" class="btn"><ion-icon name="trash"></ion-icon>Delete</button>
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

*View file*

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

*Controller file*

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

*View file*

```xml
<ion-list>
	<ion-item *ngFor="let item of items" (click)="openDetail(item.idDevice, item.nom)">
		<button ion-button color="clear" item-right (click)="pickDevice($event,item.idDevice)">
			<ion-icon [style.color]="item.disponible ? '#00CC00' : '#CD1625'" name="phone-portrait" item-center></ion-icon>
		</button>
		<h2>{{item.nom}}</h2>
	</ion-item>
</ion-list>
```

**IMPORTANT** It's important to set colour by using hexadecimal string instead of standard colour name like 'primary', 'danger' etc... because it's actually doesn't work.

*Controller file*

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

*Change button backgroundColor dynamically*

```xml
<button ion-button[style.backgroundColor]="enable ? '#00CC00' : '#FF0000'">Test</button>
```


###Pull to refresh

*View file*

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

*Controller file*

```javascript
doRefresh(refresher){
    this.users = getUsers();
    setTimeout(() => { refresher.complete(); console.log('Async operation has ended'); }, 2000); 
  }
```

##Searchbar
[Back to top](#ionic-2)  

*View file*

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

*Controller file*

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

*View file*

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

*Controller file*

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

*Style file*

```css
.home-page {
 
    .spinner-container {
        width: 100%;
        text-align: center;
        padding: 10px;
    }
 
}
```

*Data.ts provider*

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

So, by default, ionic 2 tabs project sample is using bottom navigation. To set top navigation, just change your bootstrap (in your **app.module.ts**) code by :

```
import { TabsPage } from './../pages/tabs/tabs';
import { NgModule, ErrorHandler } from '@angular/core';
import { IonicApp, IonicModule, IonicErrorHandler } from 'ionic-angular';
import { MyApp } from './app.component';

@NgModule({
  declarations: [
    MyApp,
    TabsPage
  ],
  imports: [
    IonicModule.forRoot(MyApp,{tabsPlacement: "top"})	// tab placement
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp,
    TabsPage
  ],
  providers: [{provide: ErrorHandler, useClass: IonicErrorHandler}]
})
export class AppModule {}

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
<ion-fab>
	<button ion-fab icon-only fab-bottom fab-right fab-fixed style="z-index:100">
  		<ion-icon name="add"></ion-icon>
	</button>
</ion-fab>
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

*View.html*

```xml
...
<ion-content padding>
  <ion-item>
    <ion-label>Tracking</ion-label>
    <ion-toggle id="trackingButton" black checked="false" (ionChange)="refreshTracking($event)"></ion-toggle>
  </ion-item>
</ion-content>
```

*View.ts*

```javascript
refreshTracking(e){
   console.log("refreshTracking " + e.checked);
}
```

##Popover menu
[Back to top](#ionic-2) 

Create popover menu like Evernote edit menu 

![alt tag](https://github.com/gsoulie/ionic/blob/master/popover_menu.png)

```xml
<ion-fab top right edge>
    <button ion-fab><ion-icon name="add"></ion-icon></button>
    <ion-fab-list>
      <button ion-fab><ion-icon name="logo-facebook"></ion-icon></button>
      <button ion-fab><ion-icon name="logo-twitter"></ion-icon></button>
      <button ion-fab><ion-icon name="logo-vimeo"></ion-icon></button>
      <button ion-fab><ion-icon name="logo-googleplus"></ion-icon></button>
    </ion-fab-list>
</ion-fab>
```

##Dynamic style
[Back to top](#ionic-2) 

You can dynamically change the UI component style with condition like below :

```xml
<button ion-button [style.backgroundColor]="enable ? '#00CC00' : '#FF0000'">Test</button>
```

##Toggle menu
[Back to top](#ionic-2) 

To add a toggle menu in your pages, follow the example below

*myPage.html*
```xml
<!-- here is the menu -->
<ion-menu [content]="content">
  <ion-content>
    <ion-list>
      <ion-item>A</ion-item>
      <ion-item>B</ion-item>
    </ion-list>
  </ion-content>
</ion-menu>

<!-- the page header -->
<ion-header>
  <ion-navbar color="githubviolet">
    <button ion-button menuToggle>
      <ion-icon name="menu"></ion-icon>
    </button>
    <ion-title>{{username}}</ion-title>  
     <ion-buttons end>
        <button ion-button icon-only (click)="openSearch()">
          <ion-icon name="search"></ion-icon>
        </button>
      </ion-buttons>
  </ion-navbar>
</ion-header>

<!-- page content -->
<ion-content padding class="main" #content>
	<ion-list>
		...
	</ion-list>
</ion-content>
```


#Sass
[Back to top](#ionic-2) 

Here are some tips to perform your scss 

##Positioning

###Bottom positioning
```css
.cform {
    position: absolute;
    bottom: 20%;
    left: 50px;
    right: 50px;
}
```

###Center image

```css
.image {
    position: absolute;
    left: 10px;
    right: 10px;
    display: block;
    margin-left: auto;
    margin-right: auto;
}
```
###Center component

```css
<div text-center>
	<button ion-button outline type="submit" text-center [disabled]="!f.valid">VALIDER</button>
</div>
```

#Known issues
[Back to top](#ionic-2) 

###Clicking in list item in simulator sometimes(!) doesn’t work on device

Sometimes,  on the emulator or on device, 2 out of 3 clicks it doesn't fire the click function. To solve the issue, change ```<ion-item>``` to ```<button>``` with the styling of ```ion-item```.

```xml
<ion-list>
	<button ion-item *ngFor="let audience of audience" (click)="pushProfilesList(audience)">
		<h2 class="list-title">{{audience.segment}}</h2>
		<span class="list-info">{{audience.amount}}</span>
	</button>
</ion-list>
```

###Slow tap on component and element

If you create custom components or html element and then use click handler like ```(click)="itemTap()"``` you may notice a delay if the element are not an anchor tag or button.
To fix it, add **tappable** as an attribute to you element or component like ```(click)="itemTap($event)" tappable```

see also : button role on non button clickable elements ```role="button"```

###Conflict with "this" on callback

refering to **this** has traditionally been a pain point in JavaScript. Fat arrows fix it by capturing the meaning of this from the surrounding context. So it is very useful in case of calling asynchronous callback after a window closing event.

**use case :** We want to refresh a list of items after adding a new item on it (via a "new item" modal)

*List.ts*

```javascript
...
// Refresh item list
refreshRouteList(){
    this.Db.getRoutesList().then((data)=> this.routesList = data);
}

//Open new item modal
newItem(){
    // Open DetailPage with callback function wich refresh the list after adding a new item
    /* below : traditional callback syntax --> does not work because 'this' conflict
    this.navCtrl.push(DetailPage,{callback: function(){
            this.refreshRouteList();
        }
    });*/
    
    // New syntax with Arrow function
    this.navCtrl.push(DetailPage,{callback:
        () => {this.refreshRouteList();}
    });
 }
...
```

An other solution consist in declare a variable wich contain **this** :

*List.js*

```javascript
var myThis = this;

newItem(){
    // Open DetailPage with callback function wich refresh the list after adding a new item
      
    this.navCtrl.push(DetailPage,{callback:function(){
        myThis.refreshRouteList();
    });
 }
...
```


*DetailPage.js*

```javascript
...
save(){
    this.callback(); // refreshRouteList() callback
}
...
```


#Using image
[Back to top](#ionic-2) 

To use image in your app, you can store them into ```src/app/assets/*.png```

*View file*

```xml
<img class="thb" src="{{item.image}}" item-left/>
```

*Controller file*

```javascript
let item = {name:"my item", image:"./assets/my_image.png"}
```

*Style file*

```css
.thb{
  width: 50px;
}
```


#Forms
[Back to top](#ionic-2) 

Here is a basic form sample

*View file (addPlace.html)*

```xml
<ion-content>
    <form #f="ngForm" (ngSubmit)="onSubmit(f)">
        <ion-list>
            <ion-item>
                <ion-label fixed>Title</ion-label>
                <ion-input type="text" name="title" ngModel required></ion-input>
            </ion-item>
            <ion-item>
                <ion-label floating>Description</ion-label>
                <ion-textarea name="description" ngModel required></ion-textarea>
            </ion-item>
        </ion-list>
        <ion-grid>
            <ion-row>
                <ion-col>
                    <button ion-button block outline type="button" (click)="onLocate()">Locate me</button>
                </ion-col>
                <ion-col>
                    <button ion-button block outline type="button" (click)="onOpenMap()">Select on map</button>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
                    <p>Selected place...</p>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col text-center>
                    <h5>Take a photo</h5>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
                    <button ion-button block outline type="button" (click)="onTakePhoto()">Take a photo</button>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
		<img [src]=""></img>
                </ion-col>
            </ion-row>
            <ion-row>
                <ion-col>
                    <button ion-button color="secondary" block type="submit" [disabled]="!f.valid">Add this place</button>
                </ion-col>
            </ion-row>
        </ion-grid>        
    </form>
</ion-content>
```
**note** : 
- ```type="button"``` prevent the form submition when you click on the button 
- ```type="submit"``` trigger the form submition


*Controller file (addPlace.ts)*

```javascript
import { NgForm } from "@angular/forms";
import { AddPlacePage } from "../add-place/add-place";
import { Place } from "../../models/place";
import { PlacesService } from "../../providers/places";

@Component({
	selector: "page-home",
	templateUrl: "home.html"
})
export class HomePage {
	addPlacePage = AddPlacePage;
	places: Place [] = [];
	imageUrl = "";
	location: {lat: 40.564654, lng: -73.654754};
	
	constructor() {public navCtrl: NavController, private placesService: PlacesService}
		
	onLocate(...) { this.location = ... }	// See geolocation section for detail
	
	onTakePhoto(...) { this.imageUrl = "..."; }	// See Camera section for detail
	
	onSubmit(form: NgForm) {
		// submit data
		this.placesService.addPlace(form.value.title, form.value.description, this.location, this.imageUrl);
		form.reset();
		
		this.location = {lat: 40.564654, lng: -73.654754} // initial location
		this.imageUrl = "";
	}
}
```

*Controller file (home.ts)*

```javascript
import { AddPlacePage } from "../add-place/add-place";
import { Place } from "../../models/place";
import { PlacesService } from "../../providers/places";

@Component({
	selector: "page-home",
	templateUrl: "home.html"
})
export class HomePage {
	addPlacePage = AddPlacePage;
	places: Place [] = [];
		
	constructor() {public navCtrl: NavController, private placesService: PlacesService}
	
	// Load data on page opening
	ionViewWillEnter() {
		this.places = this.placesService.loadPlaces();
	}
}
```

Now to store data, we are going to create a new service (**don't forget to add it in the app.module.ts file in provider section**)

*Service file (places.ts)*

```javascript
import { Place } from "../models/place";
import { Location } from "../models/location";

export class PlacesServices {
	private places: Place[] = [];
	
	addPlace(title: string, description: string, location: Location, imageUrl: string){
		const place = new Place(title, description, location, imageUrl);
		this.places.push(place);
	}
	
	loadPlaces(){
		return this.places.slice();	// Important : slice() return a copy of the object
	}
}
```

Displaying data in the *home* page

*View file (home.html)*

```xml
<ion-content>
	<ion-card *ngFor="let place of places" (click)="openPlace(place)">
		<img [src]="place.imageUrl"></img>
		<ion-card-content>
			<ion-card-title>{{place.title}}</ion-card-title>
			<p>{{place.description}}</p>
		</ion-card-content>
	</ion-card>
</ion-content>
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

*app.html configuration*

```html
<meta http-equiv="Content-Security-Policy" content="default-src *; script-src 'self' 'unsafe-inline' 'unsafe-eval' *; style-src  'self' 'unsafe-inline' *">
```

##Firebase
[Back to top](#ionic-2) 

###Install firebase

```
npm install --save firebase
```

Next, got to firebase and create a new app, then got to *Authentication* menu and add a new authentication method (for example Email/Password in our case). This, will generate a JSON object wich contain authentication string. Just copy the *apiKey* and *authDomain* strings and paste them in your *app.component.ts* like below :

*app.component.ts*

```javascript
...

export class MyApp {

	tabsPage = TabsPage;
	signingPage = SigninPage;
	signupPage = SignupPage;
	@ViewChild('nav') nav: NavController; //if you are using a side menu
	isAuthenticated = false;

	constructor(...) {
		firebase.initializeApp({apiKey: "<YOUR API KEY HERE>",authDomain: "<YOUR AUTH DOMAIN HERE>"});

		firebase.auth().onAuthStateChanged(user => {
			if(user) {
				this.isAuthenticated = true;
				this.rootPage = TabsPage;	// redirecting on the good page
			} else {
				this.isAuthenticated = false;
				this.rootPage = SiningPage;	// redirecting on the good page
			}
		});
	}

	// logout function
	onLogout(){
		this.authService.logOut();
		this.menuCtrl.close();
		this.nav.setRoot(SigninPage);
	}
}

```

###Authentication with firebase

Next, you need to create a new provider for firebase interaction. (Do not forget to add your new service to the *app.module.ts* in the *provider* section

*auth.ts*

```javascript
import firebase from 'firebase';
...

export class AuthService {
    signup(email: string, password: string){
        return firebase.auth().createUserWithEmailAndPassword(email, password);
    }

    signin(email: string, password: string){
        return firebase.auth().signInWithEmailAndPassword(email, password);
    }

    logout() {
	    firebase.auth().signOut();
    }

    getActiveUser(){
        return firebase.auth().currentUser;
    }
}

```
Create signin and signup forms

*signinForm.html* same as *signupForm.html*

```html
...
<ion-content>
    <form #f="ngForm" (ngSubmit)="onSignin(f)">
        <ion-list>
            <ion-item>
                <ion-label fixed>Mail</ion-label>
                <ion-input type="email" ngModel name="email" required></ion-input>
            </ion-item>
            <ion-item>
                <ion-label fixed>password</ion-label>
                <ion-input type="password" ngModel name="password" required></ion-input>
            </ion-item>
        </ion-list>
        <button ion-button block type="submit" [disabled]="!f.valid">Signin</button>
    </form>  
</ion-content>
```

*signinForm.ts*

```javascript
import { NgForm } from '@angular/forms';
import { AuthService } from '../providers/auth';
import { LoadingController, AlertController } from 'ionic-angular';

export class SigninPage {

    constructor(private authService: AuthService, 
		private loadingCtrl: LoadingController,
		private alertCtrl: AlertController){}

    // Signing method
    onSignin(form: NgForm){
        const loading = this.loadingCtrl.create({
		content: ‘signin you up…’
	});
	loading.present();
        
	this.authService.signin(form.value.email, form.value.password)
		.then(data => {
			loading.dismiss();
		})
		.catch(error => {
			loading.dismiss();
			const alert = this.alertCtrl.create({
			title: ‘signin failed’,
			message: error.message
			buttons: ['Ok']
		});

		alert.present();
    	});
    }
}

```

*signupForm.ts*

```javascript
import { NgForm } from '@angular/forms';
import { AuthService } from '../providers/auth';
import { LoadingController, AlertController } from 'ionic-angular';

export class SigninPage {

    constructor(private authService: AuthService, 
		private loadingCtrl: LoadingController,
		private alertCtrl: AlertController){}
    
    // Signup method
    onSignup(form: NgForm){
        const loading = this.loadingCtrl.create({
		content: ‘signup you up…’
	});
	loading.present();
        
	this.authService.signup(form.value.email, form.value.password)
		.then(data => {
			loading.dismiss();
		})
		.catch(error => {
			loading.dismiss();
			const alert = this.alertCtrl.create({
			title: ‘signup failed’,
			message: error.message
			buttons: ['Ok']
		});

		alert.present();
    	});
    }
}

```


###Manipulate data with firebase

####Save data

Note : Firebase is using JWT

Consider we have a *detail* page which permit to create new items.

*detail.ts*

```javascript

import { AuthService } from '../../providers/auth';
import { DataService } from '../../providers/dataservice';
...

export class ListPage {
	constructor(private dataService: DataService...){}
	
	// save data to firebase
	saveItem(){
		// Get active user token
		this.authService.getActiveUser().getToken()
		.then(
			(token: string) => {
				this.dataService.storeData(token)
				.subscribe(
					() => console.log("success"),
					error => {
						this.handleError(error.json().error);
					}
				);
			}
		);
	}
}
```
###Fetch data

Consider that we have a *list* page which display data

*list.ts*

```javascript
import { LoadingController, AlertController } from 'ionic-angular';
import { AuthService } from '../../providers/auth';
import { DataService } from '../../providers/dataservice';
import { Game } from "../../models/game";
...

export class ListPage {
	listItems: Game[];
	
	constructor(private dataService: DataService, private authService: AuthService, private loadingCtrl: LoadingController, alertCtrl: AlertController...){}
	
	// save data to firebase
	getItems(){
		const loading = this.loadingCtrl.create({content: 'please wait...'});
		loading.present();
		// Get active user token
		this.authService.getActiveUser().getToken()
		.then(
			(token: string) => {
				this.dataService.fetchData(token)
				.subscribe(
					(list: Game[]) => {
						loading.dismiss();
						if(list){
							this.listItems = list;
						} else {
							this.listItems = [];
						}
					},
					error => 
						loading.dismiss();
						this.handleError(error.json().error);
					}
				);
			}
		);
	}
	
	// Handle errors
	handleError(errorMessage: string) {
		const alert = this.alertCtrl.create({
			title: 'An error occured',
			message: errorMessage,
			buttons: ['Ok']
		});
		alert.present();
	}
}
```

###Database provider

Create a provider wich doing all database operation

*dataService.ts*

```javascript
import { ... }
import { Http, Response } from '@angular/http';
import { AuthService } from './auth';
import 'rxjs/Rx';
import { Game } from '../models/game';

@Injectable()
export class DataService {
	private itemList: Game[] = [];

	constructor(private http: Http, private authService: AuthService){}
	addItem(name: string){ this.itemList.push(new Game(name)); }
	deleteItem(index: number){ this.itemList.splice(index, 1); }
	getItems(){ 
		return this.itemList.slice(); // Important : slice() return a copy of the object
	}
	
	// Save data to firebase
	storeData(token: string) {
		// get the user Id 		
		const userId = this.authService.getActiveUser().uid;
		
		// url is available in firebase --> Database menu --> copy link
		// here we create a game-list.json in the db
		return this.http.put('https://mygames-8c67c.firebaseio.com/' + userId + '/game-list.json?auth=' + token
			, this.itemList)
		.map((response: Response) => {
			return response.json();
		});
	}
	
	// Fetching firebase data
	fetchData(token: string){
		// get the user Id 		
		const userId = this.authService.getActiveUser().uid;
	
		return this.http.put('https://mygames-8c67c.firebaseio.com/' + userId + '/game-list.json?auth=' + token)
		.map((response: Response) => {
			const game: Game[] = response.json() ? response.json() : [];
			for(let item of game) {
				if(!item.hasOwnProperty('category')) {
					item.category = [];
				}
			}
			return  game;//response.json();
		})
		.do((data) => {
			this.itemList = data 
		});
	}
}
```

*model game.ts*

```javascript
export class Game {
	constructor(public name: string, .....) {}
}
```


#Authentication
[Back to top](#ionic-2)  

##ng2-ui-auth
[Link](https://github.com/ronzeidman/ng2-ui-auth)
[Example](ng2-ui-auth-example)

##JWT
[Link](https://jwt.io/)

#Internationalization
[Back to top](#ionic-2)  

**cordova plugin installation**

```
$ cordova plugin add cordova-plugin-whitelist
```

*configure index.html*

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

*Import ng2-translate into app.js*

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

*HomePage configuration*

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

*HomePage view*

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

> Note : If splash screen doesn't showing, update your cordova plugin

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

[link : working both platform tutorial](https://medium.com/@ankushaggarwal/push-notifications-in-ionic-2-658461108c59#.tqfzfx5dd)

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

#Build for iOS
[Back to top](#ionic-2)
```
xcode-select --install
sudo npm install -g ios-deploy --unsafe-perm=true
```

*in your app folder*
```
ionic platform add ios
ionic build ios
```

For the first time, you need to open your project in XCode. To do this, navigate into your app folder and open your *.xcodeproj* file

Then, in xcode, go to Xcode -> preferences and create or connect to your apple ID. You need to create a provisioning profile or select one in the Xcode project settings tab

*Run on ios device or simulator*
```
ionic run ios
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

You will first be prompted to create a password for the keystore. Then, answer the rest of the nice tools’s questions and when it’s all done, you should have a file called **my-release-key.keystore** created in the current directory.

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


#Other modules
[Back to top](#ionic-2) 

##Make PDF
[make PDF](https://gist.github.com/scalp42/7261508)  
[tutorial](http://gonehybrid.com/how-to-create-and-display-a-pdf-file-in-your-ionic-app/)


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
