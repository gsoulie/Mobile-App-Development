#ionic 2

documentation officielle : (http://ionicframework.com/docs/v2/getting-started/migration/)

structure d'un projet ionic 2 (http://ionicframework.com/docs/v2/getting-started/tutorial/project-structure/)

ressources josh morony : (http://www.joshmorony.com/category/ionic-tutorials/)

ionic 2 n'étant pas encore déployé en version GA, il est toutefois possible de créer des projets basés sur ionic 2 en installant la beta

```$ sudo npm install -g ionic@beta```

création d'un projet compatible ionic 2

```$ ionic start myionic2project --v2```

Découvrir le tutorial ionic 2

```$ ionic start myTutorial tutorial --v2```

##Géolocalisation

(http://www.joshmorony.com/ionic-2-how-to-use-google-maps-geolocation-video-tutorial/)

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
