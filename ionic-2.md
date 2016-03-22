#ionic 2

> **Warning** this guide is based on the beta of ionic 2. Consequently, some information may be outdated

##### Table of Contents  
[Start with ionic](#start-with-ionic)  
[Atom configuration](#work-with-atom)  
[Cordova](#cordova)  
[Gulp](#gulp)  
[Useful functions](#useful-functions)  
[Angular 2](#angular-2)  
[Decorators](#decorators)  
[Config](#config)    
[Third party lib](#third-party-lib)    
[Geolocation](#geolocation)  
[TypeScript](#typescript)  
[Database](#database)  
[Camera](#camera)   
[Barcode Scanner](#barcode-scanner)  
[HTTP query](#http-query)  
[Navigation](#navigation)  
[Themes](#themes)  
[Components](#components)  
[File access](#file-access)  
[Backend Firebase](#backend-firebase)  
[Internationalization](#internationalization)  
[Publishing App](#publishing-app)  
[Splash screen and appicon](#splash-screen-and-appicon)  

##Start with ionic

**Some resources**

[ionic.io](http://docs.ionic.io/docs/io-introduction)

[Official ionic 2 documentation](http://ionicframework.com/docs/v2/getting-started/migration/)

[Official ionic 2 native component documentation](http://ionicframework.com/docs/v2/native/Calendar/)

[ionic 2 project structure](http://ionicframework.com/docs/v2/getting-started/tutorial/project-structure/)

[Josh MORONY resources](http://www.joshmorony.com/category/ionic-tutorials/)


ionic 2 is not yet available in final version, but is it possible to create ionic projects with the ionic 2 beta which can be installed as followed CLI

```
$ sudo npm install -g ionic@beta
```

**Updating ionic 2 framework**

```
$ npm install -g ionic@beta
```

**ionic 2 project creation**

```
$ ionic start myionic2project --v2
```

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

###Configuration des variables d’environement

```
nano ~/.bash_profile
```

**Configure Android environment variable** : 

```
export ANDROID_HOME=/Users/gsoulie/Library/android-sdk-macosx
export PATH=${PATH}:/Users/gsoulie/Library/android-sdk-macosx/tools:/Users/gsoulie/Library/android-sdk-macosx/platform-tools
```

**refresh bash_profile**

```
$ source .bash_profile
```

**Display log with ionic serve**

```
$ ionic serve -l -s -c
```

```
[--consolelogs|-c] ......  Print app console logs to Ionic CLI
[--serverlogs|-s] .......  Print dev server logs to Ionic CLI
[--port|-p] .............  Dev server HTTP port (8100 default)
[--livereload-port|-i] ..  Live Reload port (35729 default)
[--nobrowser|-b] ........  Disable launching a browser
[--nolivereload|-r] .....  Do not start live reload
[--noproxy|-x] ..........  Do not add proxies
```

**Testing app on multiple screen sizes and platform**

```
$ ionic serve --lab
```

##Work with Atom
[Back to top](#ionic-2) 

###1 - Install Atom

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

##Cordova
[Back to top](#ionic-2) 

**Install Cordova**

```
$ sudo npm install -g cordova
```

##Gulp
[Back to top](#ionic-2) 

Gulp package allows you to override style and theme like material design for Android

```
$ sudo npm install -g gulp
```

##Useful Functions
[Back to top](#ionic-2)  

**get specific platform**

```
var isWebView = ionic.Platform.isWebView();
var isIPad = ionic.Platform.isIPad();
var isIOS = ionic.Platform.isIOS();
var isAndroid = ionic.Platform.isAndroid();
var isWindowsPhone = ionic.Platform.isWindowsPhone();

var currentPlatform = ionic.Platform.platform();
var currentPlatformVersion = ionic.Platform.version();

ionic.Platform.exitApp(); // stops the app
```

##Angular 2
[Back to top](#ionic-2)  

[new Angular 2 concepts and syntax](http://www.joshmorony.com/ionic-2-first-look-series-new-angular-2-concepts-syntax/)
[Angular 2 syntax demistified](http://blog.thoughtram.io/angular/2015/08/11/angular-2-template-syntax-demystified-part-1.html)

AngularJS 2 is the backbone of Ionic 2, is being written for ECMAScript 6

###Some Angular 2 concepts

**Binding a Property to a value**
```
<input [value]="firstName">
```

This will set the elements property to fisrtName. More used to see ```{{firstName}}```

**Calling a Function on an Event**

```
<button (click)="someFunction($event)">
```

This will call the someFunction function and pass in the event whenever the button is clicked on. You can replace click with any native or custom event you like. You can also use the following syntax:

```
<button (^click)="someFunction($event)">
```
to make the event bubble up to other elements.

**Rendering Expressions**

```
<p>Hi, {{name}}</p>
```

Just like in Angular 1, this will evaluate the expression and render the result. There’s still some things that are the same!

**Two Way Data Binding**

In Angular 1 we could set up two way data binding by using ng-model, so if we changed a value in an input field with an ng-model it would immediately be updated elsewhere in the application if we were using that value.

We can achieve the same two way data binding in Angular 2 like this:

```
<input [value]="name" (input)="name = $event.target.value">
```

This sets the value to the expression name and when we detect the input event we updated name to be the new value that was entered. To make this easier, we can still use ng-model in Angular 2 like this to achieve the same thing:

```
<input [(ng-model)]="name">
```

**Creating a Variable to Access an Element**

```
<p #myParagraph></p>
```
This creates a local variable that we can use to access the element, so if I wanted to add some content into this paragraph I could do the following:

```
<button (click)="myParagraph.innerHTML = 'Once upon a time...'">
```

**Directives**

```
<section *ngIf="showSection">
 
<li *ngFor="#item of items">
```
We can also create embedded templates using directives like ngIf and ngFor.

**Import & Export**

ES6 allows us to Import and Export components. Take the following component for example:

```
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

```
import {HelloIonicPage} from './pages/hello-ionic/hello-ionic';
```
It’s a similar concept to Dependency Injection in Angular 1, where we would inject services we were using into the controller like this:

```
.controller('ExampleCtrl', function($scope, $state, $myService) {
```

**Promises**

ES6 adds native support for promises, which look like this:

```
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
```

rather than callbacks which can end up looking like this:

```
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

```
for (let i = 0; i < a.length; i++) {
    let x = a[i]
    //etc.
}
```
##Decorators
[Back to top](#ionic-2)  

[Decorators by Josh MORONY](https://www.joshmorony.com/building-mobile-apps-with-ionic-2/decorators-in-ionic2.html)

####@App
**@App** is the most important decorator of all, but you'll only ever use it once in each application you build. **The @App decorator declares the class that it is attached to as the root component of the application**. We've already talked about this briefly, and will continue to do so later, but the root component is essentially the starting point for your app.

It's important to understand the component based structure of an Ionic 2 application, it's basically made up of a bunch of different components tied together, and at the root of all of **this is the root component**. The root components main responsibility is setting up your root page, which will be the first page that the user sees in your application. You can then get your page to push additional pages onto the navigation stack (we will cover navigation concepts in depth in a later lesson), and those pages can in turn push more pages and so on.

####@Page
**@Page** is likely the most common decorator you will use in your applications. It is used to define any page, or "view", in your application. So if you have an application with the following pages:

Location
All Products
Product Detail
Contact

Then **each of these will be their own components which will have a decorator of @Page in the class definition**. Every page will also have a template that can either be defined directly using template in the decorator, or by using a templateUrl

####@Component

####@Directive

The @Directive decorator allows you to create your own custom directives. Typically, the decorator would look something like this:

```
@Directive({
    selector: '[my-selector]'
})
```

Then in your template you could use that selector to trigger the behaviour of the directive you have created by adding it to an element:
```
<some-element my-selector></some-element>
```
It might be a little confusing as to when to use @Component and @Directive, as they are both quite similar. The easiest thing to remember is that if you want to modify the behaviour of an existing component use a directive, if you want to create a completely new component use a component.

####@Pipe

**@Pipe** allows you to create your own custom pipes to filter data that is displayed to the user, which can be very handy. The decorator might look something like this:
```
@Pipe({
  name: 'myPipe'
})
```
which would then allow you to implement it in your templates like this:
```
<p>{{someString | myPipe}}</p>
`````
Now someString would be run through your custom myPipe before the value is output to the user.

##Config
[Back to top](#ionic-2)  

The Config lets you configure your entire app or specific platforms. You can set the tab placement, icon mode, animations, and more here.

[Config official documentation](http://ionicframework.com/docs/v2/api/config/Config/)

**sample code of Config**

```
@App({
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

```
@App({
  template: `<ion-nav [root]="root"></ion-nav>`
  config: {
    mode: 'md'
  }
})
```

You can also use the config object to define platform specific behaviour:

```
@App({
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


##Third party lib
[Back to top](#ionic-2)

###Warning not tested yet !

First, create a JS file containing your code, like :

```
export class myLib{
    constructor(){
    	// some stuff
    }
    
    function1(_params){
    	// some stuff
    }
    
    function2(){
    	// some stuff
    }
}
```

**Usage**

Add import and providers in your root page (app.js) if you want to use your lib across your project.

```
import {MyLib} from './pages/lib/myLib';

@App({
    providers: [MyLib]
    })

export class myPage{
	constructor(myLib: MyLib){	// or just constructor(myLib)
		myLib.function1("test");
	}
}
```

In child page, **providers** in **@App** is *not necessary* in your **@Page decorator**. You can use it, but it will create another myLib instance.

```
import {MyLib} from './pages/lib/myLib';

export class myPage{
	constructor(myLib: MyLib){	// or just constructor(myLib)
		this.result = myLib.function2();
	}
}
```

##Geolocation
[Back to top](#ionic-2)  

[source](http://www.joshmorony.com/ionic-2-how-to-use-google-maps-geolocation-video-tutorial/)

**Adding Google Map API depency in index.html**

```
<script src="http://maps.google.com/maps/api/js"></script>
<script src="cordova.js"></script>
<script src="build/js/app.bundle.js"></script>
```

**Important** During production deployment, you will have to create Google MAP API key and put it in parameter

**Import the new page in app.core.scss**

```
@import "pages/map/map";
```

**Loading Map (map.html)**


```
<ion-navbar *navbar>
  <ion-title>
    Map
  </ion-title>
  <ion-buttons end>
    <button (click)="addMarker()"><ion-icon name="add"></ion-icon>Add Marker</button>
  </ion-buttons>  
</ion-navbar>
 
<ion-content>
  <div id="map"></div>  
</ion-content>
```

Next, specify ion-navbar configuration in app.js
```
@App({
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

```
import {Page, Geolocation} from 'ionic/ionic';
 
@Page({
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

```
.scroll {
    height: 100%;
}
 
#map {
    width: 100%;
    height: 100%;
}
```

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-geolocation
```

**Updating loadMap function**

```
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

```
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

```
addInfoWindow(marker, content){
 
  let infoWindow = new google.maps.InfoWindow({
    content: content
  });
 
  google.maps.event.addListener(marker, 'click', function(){
    infoWindow.open(this.map, marker);
  });
 
}
```

##TypeScript
[Back to top](#ionic-2)  

##Database
[Back to top](#ionic-2)  

###First solution
There is two main solutions for data storage. The first one is the local HTML5 storage and the second is using SQLite database storage.

[source](https://www.thepolyglotdeveloper.com/2015/12/use-sqlite-in-ionic-2-instead-of-local-storage/)

####HTML5 local storage
HTML5 storage provide a key-value storage. This solution can be useful for small applications, but is not adapted for SQL querying. On the other hand, this solution is limitated to 10MB of data storage.

####SQLite database
This solution using the local device database. You can make some complex SQL query for retrieve data.

**Intallation**

After the project is created, intall cordova sqlite storage plugin

```
$ ionic plugin add cordova-sqlite-storage
```

**Database initialization (app.js)**

```
import {App, IonicApp, Platform, Storage, SqlStorage} from 'ionic-angular';
import {HomePage} from './pages/home/home';

@App({
  templateUrl: 'build/app.html',
  config: {}
})
class MyApp {
  static get parameters() {
    return [[IonicApp], [Platform]];
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

```
import {Page, App, IonicApp, Platform, Storage, SqlStorage} from 'ionic-angular';

@Page({
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

```
<ion-navbar *navbar>
    <ion-title>
        Home
    </ion-title>
    <button clear (click)="refresh()">Refresh</button>
    <button clear (click)="add()">Add</button>
</ion-navbar>
 
<ion-content class="home">
    <ion-list>
        <ion-item *ngFor="#person of people">
            {{person.firstname}} {{person.lastname}}
        </ion-item>
    </ion-list>
</ion-content>
```
###Second solution
[Back to top](#ionic-2)  

Is recommanded using **SqlStorage**. 

This is the preferred storage engine, as data will be stored in appropriate app storage, unlike Local Storage which is treated differently by the OS.

**Usage**

```
import {Injectable} from 'angular2/core';
import {Http} from 'angular2/http';
import {Storage, SqlStorage} from 'ionic/ionic';

@Injectable()
export class Record {
    constructor() {
        this.storage = new Storage(SqlStorage);
        this.storage.set('name','max');
        this.storage.set('lastname','dupont');
    }
}

storage.get('name').then((name) => {
});

// Sql storage also exposes the full engine underneath
this.storage.query('insert into projects(name, data) values("Cool Project", "blah")');
this.storage.query('select * from projects').then((resp) => {})
```

####PouchDB

First, install cordova sqlite-storage plugin

```
$ ionic plugin add cordova-sqlite-storage
```

**TODO - implementing ionic 2 sample app**

##Camera
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

```
import {Camera} from 'ionic-native';
...
...

let options = {
  quality: 100,
  destinationType: Camera.DestinationType.FILE_URI,
  sourceType: Camera.PictureSourceType.CAMERA,
  encodingType: Camera.EncodingType.JPEG,
  saveToPhotoAlbum: true
};

navigator.camera.getPicture(
  (imagePath) => {
    console.log(imagePath);
  },

  (error) => {
    console.log(error);
  }, options
);
```

**Other way**

Install typing package

```
$ npm install typings -g
```

Then execute the following command line in project's folder

```
typings install cordova --save --ambient
```

```
import {Page, NavController, Alert} from 'ionic-angular';
import {Camera} from 'ionic-native';

@Page({
  templateUrl: './build/pages/admin_page/admin_page.html'
})

export class AdminPage{
  pages: String = "pages";
  tags: String = "tags";



  page_slect_alert: {title: string};

  constructor(){
    //this.zone = ngzone;
  //  this.image = null;
    this.page_slect_alert={
      title: 'Select Fb Page For Image'

    };
  }

  stpSelect(){
    console.log('select');
  }

  getImage(){
    var options = {
      quality: 50,
			   destinationType: navigator.camera.DestinationType.FILE_URI,
			   sourceType: navigator.camera.PictureSourceType.PHOTOLIBRARY
    };

    Camera.getPicture(options).then((imageData) => {
      // imageData is either a base64 encoded string or a file URI
      // If it's base64:
      let base64Image = "data:image/jpeg;base64," + imageData;
      }, (err) => {
    });

  };

}
```

[List of camera options](https://github.com/apache/cordova-plugin-camera#module_camera.CameraOptions)


##Barcode scanner
[Back to top](#ionic-2)

[Barcode scanner documentation](http://ionicframework.com/docs/v2/native/BarcodeScanner/)

##HTTP query
[Back to top](#ionic-2)  

[source](http://www.joshmorony.com/using-http-to-fetch-remote-data-from-a-server-in-ionic-2/)

[reddit API url for testing app](https://www.reddit.com/r/gifs/top/.json?limit=10&sort=hot)

**Create the view (page.html)**

```
<ion-navbar *navbar>
  <ion-title>Tab 1</ion-title>
</ion-navbar>
 
<ion-content>
  <ion-list>
    <ion-item *ngFor="#post of posts">
      <img [src]="post.data.url" />
    </ion-item>
  </ion-list>
</ion-content>
```

**Create controller (page.js)**

```
import {Page} from 'ionic/ionic';
import {Http} from 'angular2/http';
import 'rxjs/add/operator/map';
 
@Page({
  templateUrl: 'build/pages/page/page.html'
})
export class Page {
  constructor(http: Http) {
 
    this.http = http;
    this.posts = null;
 
    this.http.get('https://www.reddit.com/r/gifs/new/.json?limit=10').map(res => res.json()).subscribe(data => {
        this.posts = data.data.children;
    });
 
  }
}
```

The **map** lib is only imported because we need is http.get function

##Navigation
[Back to top](#ionic-2)  

**Page1.html**

```
<ion-navbar *navbar>
    <ion-title>
        Other
    </ion-title>
</ion-navbar>
 
<ion-content class="other">
    <div>some content here...</div>
</ion-content>
```

**Page1.js**

```
import {Page, Platform, NavParams} from 'ionic/ionic';
 
@Page({
    templateUrl: 'app/page1/page1.html',
})
 
export class Page1Page {
    constructor(platform: Platform, navParams: NavParams) {
        this.platform = platform;
        this.navParams = navParams;
        this.firstname = navParams.get("firstname");
        this.lastname = navParams.get("lastname");
    }
}
```

**Page source (home.html)**

```
<ion-navbar *navbar>
    <ion-title>
        Home
    </ion-title>
</ion-navbar>
 
<ion-content class="home">
    <button (click)="navigate()">Navigate</button>
</ion-content>
```

**Page source (home.js)**

```
import {Page, Platform, NavController} from 'ionic/ionic';
import {OtherPage} from '../page1/page1';
 
@Page({
    templateUrl: 'app/home/home.html',
})
 
export class HomePage {
    constructor(platform: Platform, nav: NavController) {
        this.platform = platform;
        this.nav = nav;
    }
 
    navigate() {
        this.nav.push(Page1Page, {
            firstname: "Nic",
            lastname: "Raboy"
        });
    }
}
```

**Remove page from navigation**

Using ```this.nav.pop(...)```

##Themes
[Back to top](#ionic-2)  

###Statusbar

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-statusbar
```

**customization**

```
initializeApp() {
    this.platform.ready().then(() => {
       
      if (window.StatusBar) {
        //window.StatusBar.styleDefault();
        window.Statusbar.styleHex('#A81910');
        //window.Statusbar.styleColor('black');
        //window.Statusbar.hide();
        //window.Statusbar.show();
      }
    });
  }
```

**Other solution with beta3**

```
import {App, Platform} from 'ionic-angular';
import {TabsPage} from './pages/tabs/tabs';


@App({
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

##Components
[Back to top](#ionic-2)  

###Combobox

```
<div class="list">
  <label class="item item-input item-select">
    <div class="input-label">
      Lightsaber
    </div>
    <select>
      <option>Blue</option>
      <option selected>Green</option>
      <option>Red</option>
    </select>
  </label>
</div>
```

###ion-list

Solution for filling dynamic ion-list item

```
<ion-list> 
    <ion-item *ngFor="#item of items">{{item.fullname}}</ion-item> 
</ion-list>

or
```

For clickable list you have to use 

```
<ion-list> 
    <button ion-item *ngFor="#item of items">{{item.fullname}}</button> 
</ion-list>
```


**Add filter on ion-list**

Consider a ion-list in which we want to hide every items which property "deleted" is set to true

```
<ion-list>
  <ion-item-sliding *ngFor="#item of getActiveItems()" #slidingItem>
    <ion-item>{{item.fach}} ({{item.kuerzel}})</ion-item>
    <ion-item-options>
      <button (click)="showEditModal(item, slidingItem)"><ion-icon name="create"></ion-icon>Bearbeiten</button>
      <button danger (click)="doConfirm(item, slidingItem)"><ion-icon name="trash"></ion-icon>Löschen</button>
    </ion-item-options>
  </ion-item-sliding>
</ion-list>


@Page(
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

```
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


**Remove item from list**

View file
```
<ion-list>
    <ion-item-sliding *ngFor="#post of posts">
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

Controller file

```
removePost(post){
    let index = this.posts.indexOf(post);

    if(index > -1){
      this.posts.splice(index, 1);
    }
}
```

**Inifinite scroll in ion-list**

[Infinite scroll](http://ionicframework.com/docs/v2/api/components/infinite-scroll/InfiniteScroll/)

View file
```
<ion-content>

 <ion-list>
   <ion-item *ngFor="#i of items"></ion-item>
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
```
@Page({...})
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


###Customize tab icon

It's pretty easy to do actually. When you set a tabIcon property, Ionic sets a class name on the tab, based on the name you provided. So for example, if you set ```tabIcon="customicon"```, then the resulting class names will be ```.ion-ios-hygglo-customicon``` and ```.ion-ios-hygglo-customicon-outline``` (for selected tabs) for iOS. On Android, the prefix will be ```.ion-md-``` instead of ```.ion-ios-```.

Then just create a custom css, something like this:

```
.ion-ios-customicon,
.ion-md-customicon {
  content: url(../../assets/img/ui/customicon.svg);
  width: 24px;
  height: 32px;
  padding: 6px 4px 2px;
  opacity: 0.9;
}
```



##File access
[Back to top](#ionic-2)  

[source](https://forum.ionicframework.com/t/how-to-save-an-image-locally-with-ionic-2/46257/4)

##Backend Firebase
[Back to top](#ionic-2)  

###Network app sample

[source](http://www.gajotres.net/ionic-2-succesfull-oauth-social-login-with-firebase/)
[source 2](https://www.toptal.com/front-end/building-multi-platform-real-time-mobile-applications-using-ionic-framework-and-firebase)

**cordova plugin installation**

```
cordova plugin add cordova-plugin-whitelist
cordova plugin add cordova-plugin-inappbrowser@1.1.0
```

**app.html configuration**

```
<meta http-equiv="Content-Security-Policy" content="default-src *; script-src 'self' 'unsafe-inline' 'unsafe-eval' *; style-src  'self' 'unsafe-inline' *">
```

####Create Firebase account


##Internationalization
[Back to top](#ionic-2)  

**cordova plugin installation**

```
$ cordova plugin add cordova-plugin-whitelist
```

**configure index.html**

```
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

```
{
    "title" : "Internationalization Example",   
    "segment": {    
        "puppies": "Puppies",
        "kittens": "Kittens"
    }
}
```

**Import ng2-translate into app.js**

```
import {App, Platform} from 'ionic/ionic';
import {HomePage} from './pages/home/home';
import {TranslateService, TranslatePipe} from 'ng2-translate/ng2-translate';
 
 
@App({
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

```
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

```
import {Page} from 'ionic/ionic';
import {TranslateService, TranslatePipe} from 'ng2-translate/ng2-translate';
 
@Page({
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

```
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

##Publishing app
[Back to top](#ionic-2)

Now that we have a working app, we are ready to push it live to the world! Since the Ionic team already submitted the Todo app from this guide to the app store, chances are you’ll want to follow this chapter with a new app that you make on your own.

So first, we need to generate a release build of our app, targeted at each platform we wish to deploy on. Before we deploy, we should take care to adjust plugins needed during development that should not be in production mode. For example, we probably don’t want the debug console plugin enabled, so we should remove it before generating the release builds:

```
$ cordova plugin rm cordova-plugin-console
```

###Android publishing

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


##Splash screen and appicon
[Back to top](#ionic-2)

[Appicon and Splash screen documentation](http://blog.ionic.io/automating-icons-and-splash-screens/)

[Splash screen PSD](http://code.ionicframework.com/resources/splash.psd)

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
```
<preference name="FadeSplashScreen" value="false"/>
```
