#ionic 2

documentation officielle : (http://ionicframework.com/docs/v2/getting-started/migration/)

structure d'un projet ionic 2 (http://ionicframework.com/docs/v2/getting-started/tutorial/project-structure/)

ressources josh morony : (http://www.joshmorony.com/category/ionic-tutorials/)

ionic 2 n'étant pas encore déployé en version GA, il est toutefois possible de créer des projets basés sur ionic 2 en installant la beta

```$ sudo npm install -g ionic@beta```

Update du CLI en cas de MAJ du framework
```
npm install -g ionic@beta
```

création d'un projet compatible ionic 2

```$ ionic start myionic2project --v2```

Découvrir le tutorial ionic 2

```$ ionic start myTutorial tutorial --v2```

**Générer une nouvelle page dans un projet ionic 2**

```$ ionic g page myNewPage```

##Géolocalisation

source : (http://www.joshmorony.com/ionic-2-how-to-use-google-maps-geolocation-video-tutorial/)

**Ajouter les dépendances Google Map API dans le index.html**

```
<script src="http://maps.google.com/maps/api/js"></script>
<script src="cordova.js"></script>
<script src="build/js/app.bundle.js"></script>
```

**Important** Lors de la mise en production de l'application il faudra créer une clé API Google Map et renseigner cette clé en paramètre

**Importer la nouvelle page dans app.core.scss**

```
@import "pages/map/map";
```

**Charger une Map (map.html)**


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

Ensuite spécifier la configuration de la ion-navbar dans le app.js
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

**Modification du controller map.js**

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

**Style de la page (map.scss)**

```
.scroll {
    height: 100%;
}
 
#map {
    width: 100%;
    height: 100%;
}
```

**Ajout du pluging geolocation**

```
$ ionic plugin add cordova-plugin-geolocation
```

**Modification de la fonction loadMap**

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

**Ajout de marker (map.js)**

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

**Ajout fonction addInfoWindow (map.js)**

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

##Database

Deux grandes solutions sont disponibles pour le stockage de données, le stockage local HTML5 et l'utilisation de la base de données SQLite.

source : (https://www.thepolyglotdeveloper.com/2015/12/use-sqlite-in-ionic-2-instead-of-local-storage/)

#####Stockage HTML5
Le stockage HTML5 permet l'enregistrement de clé-valeurs. Cette solution peut suffire pour de petites applications mais n'est pour le requêtage SQL. D'autre part, cette solution est limitée à 10MB de données

#####Base de données SQLite
Cette solution plus classique, utilise la base de données locale du device. Elle permet le requêtage SQL.

**Intallation**

Après avoir créé le projet ionic 2, installer le plugin cordova correspondant

```$ ionic plugin add cordova-sqlite-storage```

**Initialisation de la BDD (app.js)**

```
import {App, Platform, Storage, SqlStorage} from 'ionic/ionic';
import {HomePage} from './pages/home/home';
 
@App({
    template: `
        <ion-nav [root]="root"></ion-nav>
        <ion-overlay></ion-overlay>
    `,
})
 
export class MyApp {
    constructor(platform: Platform) {
        this.platform = platform;
        this.initializeApp();
        this.root = HomePage;
    }
 
    initializeApp() {
        this.platform.ready().then(() => {
            this.storage = new Storage(SqlStorage);
            this.storage.query('CREATE TABLE IF NOT EXISTS people (id INTEGER PRIMARY KEY AUTOINCREMENT, firstname TEXT, lastname TEXT)').then((data) => {
                console.log("TABLE CREATED -> " + JSON.stringify(data.res));
            }, (error) => {
                console.log("ERROR -> " + JSON.stringify(error.err));
            });
        });
    }
}
```

**Interaction avec la BDD (home.js)**

```
import {Platform, Page, Storage, SqlStorage} from 'ionic/ionic';
 
@Page({
    templateUrl: 'build/pages/home/home.html',
})
 
export class HomePage {
    constructor(platform: Platform) {
        this.platform = platform;
        this.people = [];
        this.platform.ready().then(() => {
            this.storage = new Storage(SqlStorage);
            this.refresh();
        });
    }
 
    add() {
        this.platform.ready().then(() => {
            this.storage.query("INSERT INTO people (firstname, lastname) VALUES ('Nic', 'Raboy')").then((data) => {
                console.log(JSON.stringify(data.res));
            }, (error) => {
                console.log("ERROR -> " + JSON.stringify(error.err));
            });
        });
    }
 
    refresh() {
        this.platform.ready().then(() => {
            this.storage.query("SELECT * FROM people").then((data) => {
                this.people = [];
                if(data.res.rows.length > 0) {
                    for(var i = 0; i < data.res.rows.length; i++) {
                        this.people.push({firstname: data.res.rows.item(i).firstname, lastname: data.res.rows.item(i).lastname});
                    }
                }
            }, (error) => {
                console.log("ERROR -> " + JSON.stringify(error.err));
            });
        });
    }
}
```
**Affichage des données (home.html)**

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

##Camera

**Installation du plugin**

```
$ ionic plugin add cordova-plugin-camera
```

**Fonction pour prendre une photo**

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

##Requête HTTP

source : (http://www.joshmorony.com/using-http-to-fetch-remote-data-from-a-server-in-ionic-2/)

url du service reddit API pour le jeu de données de test : (https://www.reddit.com/r/gifs/top/.json?limit=10&sort=hot)

**Création de la Vue (page.html)**

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

**Création du controller (page.js)**

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

la lib **map** est importée uniquement parceque nous avons besoin de sa fonction http.get

##Navigation

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

**Retirer une page de la navigation**

Utiliser ```this.nav.pop(...)```

##Gestion des thèmes

###Statusbar

**installation plugin cordova**

```
$ ionic plugin add cordova-plugin-statusbar
```

**customisation**

```
var app = angular.module('ionicApp', ['ionic'])

.run(function() {
    if(window.StatusBar) {
      StatusBar.overlaysWebView(true);
      StatusBar.style(1) //Light
      StatusBar.style(2) //Black, transulcent
      StatusBar.style(3) //Black, opaque
    }
});

// styles: Default : 0, LightContent: 1, BlackTranslucent: 2, BlackOpaque: 3
$cordovaStatusbar.style(1);

// supported names: black, darkGray, lightGray, white, gray, red, green,
// blue, cyan, yellow, magenta, orange, purple, brown
$cordovaStatusbar.styleColor('black');

$cordovaStatusbar.styleHex('#000');

$cordovaStatusbar.hide();

$cordovaStatusbar.show();
```

##Composants

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

## Accès fichier

source : (https://forum.ionicframework.com/t/how-to-save-an-image-locally-with-ionic-2/46257/4)

## Backend Firebase

### Exemple social network app

source : (http://www.gajotres.net/ionic-2-succesfull-oauth-social-login-with-firebase/)
source 2 : (https://www.toptal.com/front-end/building-multi-platform-real-time-mobile-applications-using-ionic-framework-and-firebase)

**Installation plugin Cordova**

```
cordova plugin add cordova-plugin-whitelist
cordova plugin add cordova-plugin-inappbrowser@1.1.0
```

**Configuration du app.html**

```
<meta http-equiv="Content-Security-Policy" content="default-src *; script-src 'self' 'unsafe-inline' 'unsafe-eval' *; style-src  'self' 'unsafe-inline' *">
```

####Création du compte Firebase
