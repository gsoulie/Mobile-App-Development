#ionic 2

##### Table of Contents  
[Start](#start)  
[Atom configuration](#work-with-atom)  
[Cordova](#cordova)  
[Gulp](#gulp)  
[Useful functions](#useful-functions)  
[Geolocation](#geolocation)  
[TypeScript](#typescript)  
[Database](#database)  
[Camera](#camera)  
[HTTP query](#http-query)  
[Navigation](#navigation)  
[Themes](#themes)  
[Components](#components)  
[File access](#file-access)  
[Backend Firebase](#backend-firebase)  
[Internationalization](#internationalization)  

##Start

Official ionic 2 documentation : (http://ionicframework.com/docs/v2/getting-started/migration/)

ionic 2 project structure (http://ionicframework.com/docs/v2/getting-started/tutorial/project-structure/)

Josh MORONY resources : (http://www.joshmorony.com/category/ionic-tutorials/)

ionic 2 is not yet available in final version, but is it possible to create ionic projects with the ionic 2 beta which can be installed as followed CLI

```$ sudo npm install -g ionic@beta```

**Updating ionic 2 framework**

```$ npm install -g ionic@beta```

**ionic 2 project creation**

```$ ionic start myionic2project --v2```

**ionic 2 tutorial app**

```$ ionic start myTutorial tutorial --v2```

**add platform support to project**

```$ ionic platform add android```

**Generate new page in ionic 2 project**

```$ ionic g page myNewPage```

###Configuration des variables d’environement

```nano ~/.bash_profile```

**Configure Android environment variable** : 

```
export ANDROID_HOME=/Users/gsoulie/Library/android-sdk-macosx
export PATH=${PATH}:/Users/gsoulie/Library/android-sdk-macosx/tools:/Users/gsoulie/Library/android-sdk-macosx/platform-tools
```

**refresh bash_profile**

```$ source .bash_profile```

**Display log with ionic serve**

```$ ionic serve -l -s -c```

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

```$ ionic serve --lab```

##Work with Atom
[Back to top](#ionic-2) 

###1 - Install Atom

###2 - Install shell commands

Open your Atom editor and doing

*Main menu -> Install shell command*

It allows you to use ```$ apm``` command to install Atom packages

###3 - Configure Atom auto-updating

```$ apm install auto-update-packages```

Next restart Atom

###4 - Useful packages

```$ apm install atom-typescript```

```$ apm install ionic-atom```

```$ apm install atom-beautify```

##Cordova
[Back to top](#ionic-2) 

**Install Cordova**

```$ sudo npm install -g cordova```

##Gulp
[Back to top](#ionic-2) 

Gulp package allows you to override style and theme like material design for Android

```$ sudo npm install -g gulp```

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

##Geolocation
[Back to top](#ionic-2)  


source : (http://www.joshmorony.com/ionic-2-how-to-use-google-maps-geolocation-video-tutorial/)

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

source : (https://www.thepolyglotdeveloper.com/2015/12/use-sqlite-in-ionic-2-instead-of-local-storage/)

####HTML5 local storage
HTML5 storage provide a key-value storage. This solution can be useful for small applications, but is not adapted for SQL querying. On the other hand, this solution is limitated to 10MB of data storage.

####SQLite database
This solution using the local device database. You can make some complex SQL query for retrieve data.

**Intallation**

After the project is created, intall cordova sqlite storage plugin

```$ ionic plugin add cordova-sqlite-storage```

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

##Camera
[Back to top](#ionic-2)  

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-camera
```

**Taking photo**

```
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

##HTTP query
[Back to top](#ionic-2)  

source : (http://www.joshmorony.com/using-http-to-fetch-remote-data-from-a-server-in-ionic-2/)

reddit API url for testing app : (https://www.reddit.com/r/gifs/top/.json?limit=10&sort=hot)

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
```

For clickable list you have to use 

```
<ion-list> 
    <button ion-item *ngFor="#item of items">{{item.fullname}}</button> 
</ion-list>
```


##File access
[Back to top](#ionic-2)  

source : (https://forum.ionicframework.com/t/how-to-save-an-image-locally-with-ionic-2/46257/4)

##Backend Firebase
[Back to top](#ionic-2)  

###Network app sample

source : (http://www.gajotres.net/ionic-2-succesfull-oauth-social-login-with-firebase/)
source 2 : (https://www.toptal.com/front-end/building-multi-platform-real-time-mobile-applications-using-ionic-framework-and-firebase)

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
