# Angular

* [Ressources](#ressources)     
* [Notions avancées](#notions-avancees)      
* [VSCode plugins](#vscode-plugins)     
* [Généralités](#généralités)     
* [Commandes](#commandes)     
* [Update angular](#update-angular)     
* [Best practices](#best-practices)     
* [Spread & Rest operators](#spread-&-res-operators)     
* [Object destructuration](#object-destructuration)     
* [Angular project lifecycle](#angular-project-lifecycle)     
* [Components interactions](#components-interactions)     
* [Directive structurelle ng-template](#directive-structurelle)     
* [Typescript](#typescript)     
* [Web worker](#web-worker)     
* [injection de dépendance (services)](#)     
* [Promise](#promise)     
* [Observable](#observable)      
* [RxJs ](#rxjs)     
* [Codes retour http](#codes-retour-http)     
* [Form](#form)     
* [ViewChild](#viewchild)     
* [Composants gratuits](#composants-gratuits)     
* [Routing](#routing)     
* [Tests unitaires](#tests-unitaires)     
* [Directives](#directives)     
* [UI frameworks](#ui-frameworks)     
* [Theming](#theming)     
* [Adapter pattern](#adapter-pattern)     
* [Flex layout](#flex-layout)        
* [ng-content](#ng-content)      
* [workspace](#workspace)      


## Ressources

https://alligator.io/angular/    
https://blog.thoughtram.io/    
https://nitayneeman.com/posts/all-talks-from-ng-conf-2018/    

## Notions avancées

[composant extend/collapse générique avec boucle de composants](https://makina-corpus.com/blog/metier/2019/des-boucles-generiques-de-composants-avec-angular)         
[content projection - attention ne fonctionne PAS avec les boucles](https://codecraft.tv/courses/angular/components/content-projection/)        

## VSCode plugins
[Back to top](#angular) 

Angular schematics    
Auto import    
typescript hero => permet de créer des compos / pipe etc... en faisant un clic droit plutôt que la console    
tslint / eslint    

## Généralités

### Les 3 fichiers principaux pour créer une appli angular
[Back to top](#angular) 

main.ts permet de définir le type d'application (mobile, web, ...). Ensuite il appelle le module racine (AppModule)
app.module.ts
app.component.ts

### Cycle de vie d'un composant

| Order   |
|----------|
|constructor|
|nbOnChanges|
|ngOnInit|
|ngDoCheck|
|ngAfterContentInit|
|ngAfterContentChecked|
|ngAfterViewInit|
|ngAfterViewChecked|

### Découpage projet

````
app
 |-- home
 |-- user
 |-- |-- userList
 |-- |-- userDetail
 |-- |-- user.component.ts
 |-- |-- user.component.html
 |-- |-- user.component.css
 |-- |-- user.routes.ts
 |-- ticket
 |-- |-- ticketList
 |-- |-- addTicket
 |-- Login
 |-- shared
 |-- |-- class
 |-- |-- cst
 |-- |-- ...
 |-- pipes
 |-- services
 |-- app.component.html
 |-- app.component.ts
 |-- app.component.css
 |-- app.module.ts
 ````

## Commandes

````
ng g c components/home --module app
ng g s shared/services/myService --skipTests
````

## Update angular
[Back to top](#angular) 

To update Angular CLI to a new version, you must update both the global package and your project's local package.

note : lancer l'invité de commande en mode administrateur

````
Global package:

npm uninstall -g @angular/cli
npm cache verify
# if npm version is < 5 then use `npm cache clean` 
npm install -g @angular/cli@latest
Local project package:

rm -rf node_modules dist # use rmdir /S/Q node_modules dist in Windows Command Prompt; use rm -r -fo node_modules,dist in Windows PowerShell 
npm install --save-dev @angular/cli@latest
npm install
````

### Solution 2
The Angular team recommends updating the CLI and Core first:

````$ ng update @angular/cli @angular/core````
Afterward, update the rest of the Angular packages if there are no errors.

Another resource to check out is the Angular update guide: https://update.angular.io. Select the version your app is currently on, then the version you’re updating to. The guide will show you what to do before, during, and after the update. In my experience, updating is painless since there’s very little manual work to do. 


## Best practices
[Back to top](#angular) 

### Model Adapter Pattern

Utiliser au maximum cette technique (#adapter-pattern) pour gagner en maintenabilité

### Blocs conditionnels

Il est bien d'encadrer les blocs conditionnels *ngIf* avec des **ng-content**

````
<ng-container *ngIf="requestLoading">
     <app-loading></app-loading>
</ng-container>

<ng-container *ngIf="!requestLoading">
     <button type="submit" *ngIf="!isEdit" [disabled]="!formTicket.valid" (click)="create()">Créer</button>
     <button type="submit" *ngIf="isEdit" [disabled]="!formTicket.valid" (click)="edit()">Editer</button>
</ng-container>
````

### Pipe

Tout traitement qui modifie la vue doit préférablement utiliser les pipes plutôt qu'une méthode. Les pipes sont très optimisés et offrent un gain de performance énorme.

### Optimisation lancement application
[Back to top](#angular) 

1 - lazy loading
ne charger que les routes nécessaires au démarrage

2 - server side rendering
faire une capture de la page côté backend et l'envoyer au client, pendant ce temps là, angular charge le reste.
C'est juste une capture, le client ne peut pas intérragir. C'est juste en attendant.
cf : https://angular.io/guide/universal

### zone.js
[Back to top](#angular) 

Un changeDetector par composant. Il gère pour chacun les 3 zones à écouter (events, timers, network).
Par défaut, Angular écoûte les 3 zones de chacun en permanence.

zone *Event* : événement utilisateur (click, entrée clavier etc...)
zone *Timers* : setTimeout() et setInterval()
zone *Network*: Appel http

**BONNE PRATIQUE** mettre tous les composants en mode *OnPush()* c'est un gain d'optimisation important.
Il va faloir ensuite provoquer la mise à jour de la vue à la main.
Ajouter dans le code suivant 
````
@Component{
	changeDetection: ChangeDetectionStrategy.OnPush;	// il ne va écouter QUE la zone event
}
````

Ce mode est **hérité par tous les enfants**. Car le changeDetector hérite de la stratégie du père.
Donc il suffit de le déclarer dans le père et il n'y aura pas besoin de le déclarer dans les enfants

Le mode OnPush est utilisé pour écouter la zone Event uniquement. Le mode Default écoute toutes les zones.

Pour forcer le déclenchement à la main il faudra utiliser 

````
constructor(private ref: ChangeDetectorRef) {

	setInterval(() => {
		this.increase ++;
		this.ref.markForCheck(); // demande à Angular de forcer le refresh. Il le fera quand il aura un peu de temps et met à jour toute la branche concernée (père et tous les enfants)
	}, 1000);

}
````

On peut aussi utiliser 
````this.ref.detectChanges(); // force le refresh maintenant lors de l'appel et ne met à jour que le compo actif et ses enfants````

Le **markForCheck** est un markage. On dit à ANgular, quand tu as le temps, rafraichi toute la branche (du père au dernier fils)

Le **detectChanges** est instantané, on force Angular à rafraichir tout de suite le composant en cours et ses enfants.

L'utilisation de l'un ou l'autre est à voir au cas par cas mais de manière générale, préférer le markForCheck qui est moins violent car c'est Angular qui le gère.

### Detacher - Réattacher 

On peut aussi manuellement désactiver / réactiver l'écoute des zones pour un composant avec :

````
this.cd.detach();	// ne sera plus mis à jour
this.cd.reattach();	// se remet à jour
````

## Spread & Rest operators
[Back to top](#angular) 

````
let arr = [1, 2, 3]; 

// let arr2 = [...arr, 4, 5] => [...[1, 2, 3], 4, 5] => [1, 2, 3, 4, 5]

let arr2 = [...arr, 4, 5]; // SPREAD

console.log(arr2); // [1, 2, 3, 4, 5]

let obj = {a: 1, b: 2};

let obj2 = {...obj, c: 3};

console.log(obj2); // {a: 1, b: 2, c: 3}
````

## Object destructuration
[Back to top](#angular) 

````
const user = [{nom: 'toto', prenom: 'paul'},{nom: 'titi', prenom: 'luc'}];
let [o1, o2] = user;
````

### Function parameters destructuration
[Back to top](#angular) 

````
maFunct = ({param1, param2}) {

}

maFunct({param2: 5, param1: 1});
````

==> permet de s'affranchir de l'ordre des paramètres et de gérer plus facilement les 
paramètres optionnels

## Angular project lifecycle
[Back to top](#angular) 

1 - main.ts
2 - app.module.ts => déclare tous les composants/directive/pipe/services de l'appli
3 - app.component.ts => c'est le bootstrap component

## Components interactions
[Back to top](#angular) 

Angular fonction en single way data-binding, c'est à dire que les enfants ne peuvent communiquer qu'avec leur parent direct. C'est donc le parent qui transmet ses propriété via un @Input. Si l'enfant souhaite modifier une valeur, il doit en notifier son parent via un Event Emitter dans avec un @Output

### @Input

**Enfant**

Propriété dans composant enfant

````
@Input() public user: Object;

<input type="text" [(ngModel)]="user.name" />
````

**Parent**

````
<app-compo-enfant [user]="myUser"></app-compo-enfant>

myUser: Object

ngOnInit() {
	this.myUser = {
		name: 'Mon user'
	}
}
````


> //!\\ l'enfant ne peut pas modifier l'objet fourni par le parent !
Si l'enfant modifie l'objet, il doit remonter l'information au père avec event emitter

### Event emitter
[Back to top](#angular) 

**Enfant**

````
@Output() vider = new EventEmitter();

public vider() {
	this.vider.emit('param de retour');
}

// on peut éviter de créer une méthode relais 
// en appelant directement emit dans la vue
<button (click)="vider.emit()">vider</button>
<!-- <button (click)="vider()">vider</button>-->
````

**Parent**

````
<app-compo-enfant (vider)="onVider($event)">

public onVider(val) {
	this.user = { name: val }
}
````

## Directive structurelle
[Back to top](#angular) 

````
<p *ngIf="name; else noName">
	cas name non vide
</p>


<ng-template #noName>
	cas else
</ng-template>
````

Rq : *ngIf avec else est équivalent à double blocs *ngIf

*Autre exemple*

````
<ng-container *ngIf="tickets; then okTickets else noTickets"></ng-container>

<ng-template #okTickets>
 <div *ngFor="let ticket of tickets; let i = index" class="ticket">
    <div class="actions" *ngIf="!loadingRequest">
	<span class="remove" (click)="removeTicket(i)">X</span>
	<span class="edit" (click)="editTicket(i)">| Edit |</span>
    </div>

    <div class="left">
	<img [src]="ticket.urlImage"/>
    </div>
 </div>
</ng-template>
````

### mots clés réservés de ngFor 

Il existe trois mots clés pour le ngFor : *index, first, last*
````
<p *ngFor="let item of items; i = index; isFirst = first; isLast = last">

<b *ngIf="isFirst">je suis premier</b>
````

## Typescript
[Back to top](#angular) 

codage en TS qui sera transpilé en JS car le navigateur ne sait pas interpreter le TS

## Web worker
[Back to top](#angular) 

Webworker permet de déleguer une tâche lourde (ex afficher un objet 3D calculé). Cela permet au thread principal, d'alléger sa mémoire
et de déléguer les tâches lourdes au webworker qui va s'en charger?


## injection de dépendance (services)
[Back to top](#angular) 

permet de pallier la communication entre un compo 1 avec un compo 100. 
Cela évite de passer 99 input et remonter par 99 output

les injections de dépendance sont ce qu'on appelle les services 

````
constructor(private monService: MonService){}

maFunct() {
	this.monService.getData();
}
````

## Promise
[Back to top](#angular) 

````
let promise = new Promise((resolve, reject) => {
	setTimeout(() => {
		resolve('résultat promise');
	}, 2000);
});

promise.then((data) => {
	console.log(data);
})
.catch((error) => {console.error(error);});
````

## Observable
[Back to top](#angular) 

https://makina-corpus.com/blog/metier/2017/premiers-pas-avec-rxjs-dans-angular       
https://guide-angular.wishtack.io/angular/observables/creation-dun-observable

## RxJs 
[Back to top](#angular) 

https://rxjs-dev.firebaseapp.com/guide/subject
https://makina-corpus.com/blog/metier/2017/premiers-pas-avec-rxjs-dans-angular

## Codes retour http
[Back to top](#angular) 

faire toujours une surcouche à httpclient voir APIHelper correction TP2

catch récupérer code erreur et le traiter dans ton service surcouche (retourner un enum) et interpréter
redirige l'erreur vers le composant concerné

## Form
[Back to top](#angular) 

**Template-driven** : la logique de validation du formulaire est dans la vue (C'EST MAL la vue ne doit faire QUE de la vue !)

**Model-driven-form** : la logique est dans le controller c'est la **bonne pratique** !!

Il utilise des FormGroup qui contiennent d'autres FormGroup ainsi que des FormControl. Le FormGroup permet de définir la logique pour tout un formulaire.
Le FormControl définit la logique d'un input du FormGroup

Pour faciliter l'écriture des formulaires, utiliser Angular FormBuilder : https://angular.io/guide/reactive-forms

### FormBuilder

Permet de simplifier l'écriture des formulaires ReactiveForm

````
loginForm: FormGroup;

// Méthode avec FormBuilder
constructor (private fb: FormBuilder) { }

this.loginForm = this.fb.group({
	login: [isDevMode() ? 'admin' : '', Validators.required],
	password: [isDevMode() ? 'password' : '', Validators.required]
});

// Méthode sans FormBuilder

this.loginForm = new FormGroup({
	login: new FormControl('admin', Validators.required),
	password: new FormControl('password', Validators.required)
});
````

### Custom validator
[Back to top](#angular) 

#### Validator asynchrone

retourne null si tout va bien et retourne un objet en cas d'erreur.

**ATTENTION** Ne jamais faire de *reject* mais un *resolve(<quelque-chose>)* en cas d'erreur

Un validator custom est une classe dans lequel on défini une methode statique.
=> this.champ = new FormControl(null, monvalidator.saMethodeStatique);

## ViewChild
[Back to top](#angular) 

Permet de contrôler un élément de la vue, depuis le controller

````
@ViewChild('userForm', {static: true}) monUserForm: NgForm;
//{static: true/false} => Avoir le droit d'y accéder avant (true) ou après (false) que la vue ne soit prête
````

## Composants gratuits
[Back to top](#angular) 

codepen.io

## Routing
[Back to top](#angular) 

route par défaut, doit toujours être à la fin du fichier de routing !!

````
{
	redirectTo: '/default',
	path: '**'
}
````

**A savoir :** *href* recharge la page, pas le *routerLink*

### Deep linking - routes enfants

Deux solution : 

- Définir les childroutes dans le app.route.ts
- Créer un fichier route dans chaque composant qui aura besoin de routes enfant. **Bonne pratique**

La seconde solution est une meilleure pratique pour éviter d'avoir un fichier app.routes.ts trop conséquent.

*app.routes.ts*
````
export const APP_ROUTES: Routes = [
	{
		path: 'home'
		component: HomeComponent,
		children: HOME_ROUTES
	}
]
````

*home.routes.ts*
````
export const HOME_ROUTES: Routes = [
	{
		path: 'child1'
		component: ChildComponent
	},
	{
		path: 'child2'
		component: ChildComponent
	},

	},
	{
		redirectTo: '/default',
		path: '**'
	}
]
````
Ajoute ensuite le router-outlet du Home

*home.component.html*
````
<router-outlet></router-outlet>
````

### Naviguer depuis la vue
[Back to top](#angular) 

Syntaxes possibles :
````
<button [routerLink]="['./login']">Navigate</button> <!-- tableau de routes -->
<button routerLink="/login">Navigate</button> <!-- route seule -->
<button [routerLink]="['./client', 'product']">Navigate</button> <!-- concatène les 2 routes avec un / automatiquement -->
<button [routerLink]="['/client', client.id]">Navigate</button> <!-- routing avec paramètres -->
<button routerLink="/client/{{ client.id }}">Navigate</button> <!-- routing avec paramètres idem syntaxe ci-dessus -->
<button [routerLink]="['/client', { foo: 'foo' }]">Navigate</button>
<button [routerLink]="['area', businessArea, 'projects']"</button>
````

**routerLinkActive**

Vérifie si l'itinéraire lié d'un élément est actuellement actif et vous permet de spécifier une ou plusieurs classes CSS à ajouter à l'élément lorsque l'itinéraire lié est actif.

````
<a routerLink="/first-component" routerLinkActive="active">
````

*Exemple*

Chaque fois que l'URL est */user* ou */user/bob*, la classe *active-link* est ajoutée à la balise d'ancrage. Si l'URL change, la classe est supprimée.

````
<a routerLink="/user/bob" routerLinkActive="active-link">Bob</a>
````

On peut aussi définir plusieurs classes à l'aide d'une chaîne séparée par des espaces ou d'un tableau. 
````
<a routerLink="/user/bob" routerLinkActive="class1 class2">Bob</a>
<a routerLink="/user/bob" [routerLinkActive]="['class1', 'class2']">Bob</a>
````

### Routing parameters
[Back to top](#angular) 

````
{
	path: 'ticket/edit/:id'
	component: TicketComponent
}
````

### Naviguer depuis le controller
[Back to top](#angular) 

````
this.route.navigate(['./ticket', 'edit', idTicket], {relativeTo: this.activatedRoute});	// => /ticket/edit/12
````

*Récupérer les paramètres de route dans le controller*
````
ngOnInit() {
	//this.ticketId = this.activatedRoute.snapshot.params.id // ATTENTION one shot !! ne sera plus mis à jour
	this.activatedRoute.params.subscribe((params) => {
		this.ticketId = params.idTicket;
	});
}
````

> **IMPORTANT** - **BONNE PRATIQUE** : il faut récupérer le paramètre dans un observable pour éviter la problématique d'appel multiple d'une même route avec un paramètre différent. En effet Angular ne recréé pas un composant si on vient déjà de ce dernier. De fait il ne rééxécute pas la logique codée dans ngOnInit() (appel ws pour récupération des données par exemple).

### Lazy-loading routes
[Back to top](#angular) 

C'est webpack qui va prendre en charge le lazy loading et créer un chunk du module

*Syntaxe Angular 8*
````
{
	path: 'tickets',
	loadChildren:() => import('./lazy/Lazy.module').then(m=>m.NomModule)
}
````

#### Preloading
[Back to top](#angular) 

Permet en background d'une page, de charger le contenu des autres pages

### router-outlet multiple
[Back to top](#angular) 

On peut définir plusieurs <router-outlet>. Mais faire **ATTENTION** de bien les nommer différemment

https://www.techiediaries.com/angular-router-multiple-outlets/

### Guards
[Back to top](#angular) 

Le guard retourne toujours un boolean. Soit un boolean directement, soit une promise qui retourne un boolean, soit un observable qui retourne un boolean

````
CanActivate() {
	return this.isLogged().then((res) => {
		if(res){
			return true;
		} else {
			this.router.navigate(['./login']);
			return false;
		}
	}
}
````

**CanDeactivate** permet de vérifier si j'ai le droit de quitter la route actuelle. C'est utilisé dans le cas ou l'utilisaateur est entrain de modifier un formulaire par exemple.

### Connaître la route depuis laquelle on vient

````
private routerEventsSubscription: Subscription;

ngOnInit() {
// On détecte les changements d'URL pour ne pas afficher les boutons de navigation vers la page sur laquelle on est déjà
    this.routerEventsSubscription = this.router.events.subscribe(() => {
      this.isOnLoginPage = this.router.url === '/login';
      this.isOnHomePage = this.router.url === '/home';
    });
}
````

### Tab Routing with routing back from modale
[Back to top](#angular)

Here is a full sample of tab routing with routing back integration from child modale. 

Use case : main page *home-tabs* gets 3 tabs (home, queries, lists). From *queries* and *lists* tabs we have a button which open a new modale named *results*

*app.routing.module.ts*
```
// Contains the route of the home-tabs page
const routes: Routes = [
 
  {
    path: '',
    loadChildren: () => import('./home-tabs/home-tabs.module').then( m => m.HomeTabsPageModule)
  },
]
```

*home-tabs-routing.module.ts*

````
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { QueriesPage } from '../pages/queries/queries.page';
import { HomeTabsPage } from './home-tabs.page';

const routes: Routes = [
  {
    path: '',
    component: HomeTabsPage,
    children: [
      {
        path: 'home',
        loadChildren: () => import('./../pages/home/home.module').then(m => m.HomePageModule)
      },
      {
        path: 'queries',
        children: [
          {
            path: '',
            loadChildren: () => import('./../pages/queries/queries.module').then(m => m.QueriesPageModule)
          },
          {
            path: 'results/:queryId',	// in this case we want to pass a parameter
            loadChildren: () => import('./../pages/results/results.module').then( m => m.ResultsPageModule)
          }
        ]
      },
      {
        path: 'lists',
        children: [
          {
            path: '',
            loadChildren: () => import('./../pages/lists/lists.module').then(m => m.ListsPageModule)
          },
          {
            path: 'results',
            loadChildren: () => import('./../pages/results/results.module').then( m => m.ResultsPageModule)
          }
        ]
        
      },
    ]
  },
  {
    path: '',
    redirectTo: '/home',
    pathMatch: 'full'
  },
 
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule],
})
export class HomeTabsPageRoutingModule {}

````

Navigate on *results* modale 

````
// Navigating from queries page 
<ion-item tappable routerLink="results/{{ item.queryId }}" routerDirection="forward">

// Navigating from lists page
<ion-button routerLink="results">results</ion-button>
````

Routing back from modale to current tab

````
<ion-header>
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-back-button></ion-back-button>
    </ion-buttons>
  </ion-toolbar>
</ion-header>
````

## Tests unitaires
[Back to top](#angular) 
Karma 

Jasmine

Lancer les tests
````
ng test
````

## Directives
[Back to top](#angular) 

Lss directives permettent de modifier les éléments du DOM. **Leur responsabilité est relative à la vue**

Dans l'idéal :
- Si on **modifie l'aspect** d'un élément on utilise une **directive**. 
- SI on **créé un élément** alors on utilise un **component**

*Appel d'une directive (ici : appHighlight)*
````
<div appHighlight (click)="maFonction()">TEXT</div>

<!-- Une directive peut aussi envoyer un EventEmitter -->
<div appHighlight (eventDirective)="gererEmitterDeLaDirective()">TEXT</div>
````

*Directive qui applique un fond rouge sur un click de la div*
````
@Directive({
	selector: '[appHighlight]'
})

export class HighlightDirective {
	constuctor(private _element: ElementRef) { }

	// Ecouter événement click. Sur un click il applique la fonction onClick()
	@HostListener('click') 
	onClick(){
		this._element.nativeElement.style.backgroundColor = 
		this._element.nativeElement.style.backgroundColor ? null : 'red';
	}
}
````

### Ajouter des propriétés à une directive
[Back to top](#angular) 

````
<div [appHighlight]="'red'" [isMaj]="true"">TEXT</div>
````

*Directive qui applique un fond rouge sur un click de la div*
````
@Directive({
	selector: '[appHighlight]'
})

export class HighlightDirective {
	@Input('appHighlight') actualColorText: string;
	@Input() isMaj: boolean;

	constuctor(private _element: ElementRef) { }

	onClick(){
		const colorToApply = this.actualColorText || 'green';
		this._element.nativeElement.style.backgroundColor = 
		colorToApply;
	
		if(this.isMaj) {
			this._element.nativeElement.style.textTransform = 'uppercase';
		}
	}
}
````

### ngclass
Selon le contexte, si un traitement conditionnel est utilisé plusieurs fois dans l'appli et/ou avec de l'algo à faire, utiliser une directive.

Si c'est un cas très ponctuel, utiliser ````[ngClass]````


### ng-content
[Back to top](#angular)    
https://wizbii.tech/un-layout-dynamique-avec-ng-content-d00e27ab26d9

````<ng-content></ng-content>````

## UI frameworks
[Back to top](#angular)      

[officials links](https://angular.io/resources?category=development)       

Best 4       
[official] https://material.angular.io/guide/getting-started       
https://valor-software.com/ngx-bootstrap/#/documentation       
https://primefaces.org/primeng/showcase/#/setup        
https://ng-bootstrap.github.io/#/home       
       
http://ng-lightning.github.io/ng-lightning/#/get-started       
https://ng.ant.design/components/button/en        
http://ng.mobile.ant.design/#/docs/getting-started/en      
https://alyle.io/getting-started/installation       

### Material icons

Liste des icônes Material : https://www.angularjswiki.com/fr/angular/angular-material-icons-list-mat-icon-list/       

### Material Angular

Pour faciliter la gestion des composants material :

Créer un fichier **material.module.ts** dans le répertoire **app** (avec app.module.ts) dans lequel on va importer tous les modules material nécessaire ex :

> ATTENTION : selon la version d'angular, tous les composants ne sont pas à importer depuis *@angular/material* bien vérifier dans la doc

````
import {NgModule} from '@angular/core';
import {FormsModule, ReactiveFormsModule} from '@angular/forms';
import {BrowserAnimationsModule} from '@angular/platform-browser/animations';

import {
  MatIconModule,
  MatButtonModule,
  MatInputModule,
  MatAutocompleteModule,
  MatChipsModule,
  MatListModule,
  MatGridListModule,
  MatExpansionModule,
  MatToolbarModule,
  MatProgressSpinnerModule,
  MatDialogModule,
  MatTooltipModule,
  MatMenuModule,
  MatCardModule,
  MatSelectModule,
  MatCheckboxModule,
  MatTableModule,
  MatDatepickerModule,
  MatNativeDateModule,
} from '@angular/material';


@NgModule({
  exports: [
    FormsModule,
    BrowserAnimationsModule,
    ReactiveFormsModule,
    MatIconModule,
    MatButtonModule,
    MatInputModule,
    MatAutocompleteModule,
    MatChipsModule,
    MatListModule,
    MatGridListModule,
    MatExpansionModule,
    MatToolbarModule,
    MatProgressSpinnerModule,
    MatDialogModule,
    MatTooltipModule,
    MatMenuModule,
    MatCardModule,
    MatSelectModule,
    MatCheckboxModule,
    MatTableModule,
    MatDatepickerModule,
    MatNativeDateModule
  ]
})
export class AppMaterialModule {}
````

Ensuite importer ce fichier dans le **app.module.ts**

````
import { HomeComponent } from './components/home/home.component';
import { AppMaterialModule } from './material.module';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    AppMaterialModule,
    BrowserAnimationsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

````

*Exemple d'utilisation*

````
  <mat-toolbar color="primary">
    <button mat-icon-button class="example-icon" aria-label="Example icon-button with menu icon">
      <mat-icon>menu</mat-icon>
    </button>
    <span>Home</span>
    <span class="example-spacer"></span>
    <button mat-icon-button class="example-icon favorite-icon" aria-label="Example icon-button with heart icon">
      <mat-icon>favorite</mat-icon>
    </button>
    <button mat-icon-button class="example-icon" aria-label="Example icon-button with share icon">
      <mat-icon>share</mat-icon>
    </button>
  </mat-toolbar>
````


## Theming
[Back to top](#angular)   

[Documentation](https://material.angular.io/guide/theming)     

Créer un fichier src/mon-theme.scss contenant la structure suivante (attention le fichier doit être de type **scss**):

````
@import '~@angular/material/theming';
@include mat-core();

// Define the palettes for your theme using the Material Design palettes available in palette.scss
// (imported above). For each palette, you can optionally specify a default, lighter, and darker
// hue. Available color palettes: https://material.io/design/color/
$my-app-primary: mat-palette($mat-green);
$my-app-accent:  mat-palette($mat-pink, A200, A100, A400);

// The warn palette is optional (defaults to red).
$my-app-warn:    mat-palette($mat-red);

// Create the theme object. A theme consists of configurations for individual
// theming systems such as `color` or `typography`.
$my-app-theme: mat-light-theme($my-app-primary, $my-app-accent, $my-app-warn);

// Include theme styles for core and each component used in your app.
// Alternatively, you can import and @include the theme mixins for each component
// that you are using.
@include angular-material-theme($my-app-theme);

.alternate-theme {
  $alternate-primary: mat-palette($mat-light-blue);
  $alternate-accent:  mat-palette($mat-yellow, 400);
  $alternate-theme: mat-light-theme($alternate-primary, $alternate-accent);
  @include angular-material-theme($alternate-theme);
}

````

Mettre à jour le *angular.json* pour pointer sur ce fichier thème

````
"styles": [
      {
	"input": "src/mon-theme.scss"
      },
      "src/styles.scss"
],
````

*Utilisation*

````
<mat-card>
      Main Theme:
      <button mat-raised-button color="primary">
        Primary
      </button>
      <button mat-raised-button color="accent">
        Accent
      </button>
      <button mat-raised-button color="warn">
        Warning
      </button>
    </mat-card>
    <br>
    <mat-card class="alternate-theme">
      Alternate Theme:
      <button mat-raised-button color="primary">
        Primary
      </button>
      <button mat-raised-button color="accent">
        Accent
      </button>
      <button mat-raised-button color="warn">
        Warning
      </button>
</mat-card>
````

## Adapter pattern
[Back to top](#angular)      
Le Model Adapter Pattern permet de simplifier le code des retours d'observable et aussi de respecter la pratique du DRY (Don't repeat yourself)

https://florimond.dev/blog/articles/2018/09/consuming-apis-in-angular-the-model-adapter-pattern/

The aim is to simplify the following code : 

*course.model.ts*
````
export class Course {
  constructor(
    public id: number,
    public code: string,
    public name: string,
    public created: Date
  ) {}
}
````

*course.service.ts*
````
export class CourseService {
  private baseUrl = "http://api.myapp.com/courses";

  constructor(private http: HttpClient) {}

  // return list of courses
  list(): Observable<Course[]> {
    const url = `${this.baseUrl}/`;
    return this.http
      .get(url)
      .pipe(
        map((data: any[]) =>
          data.map(
            (item: any) =>
              new Course(item.id, item.code, item.name, new Date(item.created))
          )
        )
      );
  }
}
````

By creating an Adapter : 


*course.model.ts*
````
import { Injectable } from "@angular/core";
import { Adapter } from "./adapter";

export class Course {
  // ...
}

@Injectable({
  providedIn: "root",
})
export class CourseAdapter implements Adapter<Course> {
  adapt(item: any): Course {
    return new Course(item.id, item.code, item.name, new Date(item.created));
  }
}
````

*course.service.ts*
````
export class CourseService {
  private baseUrl = "http://api.myapp.com/courses";

  constructor(private http: HttpClient, private adapter: CourseAdapter) {}

  list(): Observable<Course[]> {
    const url = `${this.baseUrl}/`;
    return this.http.get(url).pipe(
      // Adapt each item in the raw data array
      map((data: any[]) => data.map((item) => this.adapter.adapt(item)))
    );
  }
}
````

This helps to be more adaptive if the backend makes changes on the object format.

For example, if the backend changes "name" by "label", we just have to modify our adapter class without changing anything else in our code.

*course.model.ts*
````
@Injectable({
  providedIn: 'root'
})
export class CourseAdapter implements Adapter<Course> {

  adapt(item: any): Course {
    return new Course(
      item.id,
      item.code,
-     item.name,
+     item.label,
      new Date(item.created),
    );
  }
}
````

## Flex layout
[Back to top](#angular)       

[Tutorial flex-layout](https://zoaibkhan.com/blog/create-a-responsive-card-grid-in-angular-using-flex-layout-part-1/)       
[Flex-layout Demos](https://tburleson-layouts-demos.firebaseapp.com/#/responsive)      
[Documentation](https://github.com/angular/flex-layout/wiki/API-Documentation)      

### installation

````
npm install -s @angular/flex-layout
````

## ng-content
[Back to top](#angular)

La balise <ng-content> permet de définir un modèle de vue fixe et de définir un emplacement pour du contenu dynamique.
Par exemple, imaginons un template dans lequel on aurait un header et du contenu :

*layout.component.ts*
````
import { Component, Input, Output } from '@angular/core';
@Component({
  selector: 'app-layout',
  templateUrl: 'card.component.html',
})
export class LayoutComponent {
    @Input() header: string = 'this is header';   
}
````

*layout.component.html*
````
<section class="layout">
    <h2 class="layout__header">
        {{ header }}
    </h2>
    <!-- slot de transclusion -->
    <div class="layout__content">    
        <ng-content></ng-content>
    </div>
</section>
````
	
Maintenant, utilisons ce layout dans un autre composant :

*articles.component.html*
````
<h1>Notre super App !</h1>
<app-layout header="Le header de mon layout !">
    <!-- début du contenu dynamique : -->
    <article class="content__article">
       <h2>Article 1</h2>
       <p>Mon super résumé...</p>
    </article>
    <!-- fin du contenu dynamique -->
<app-layout>
````
	
Et voilà ! Le slot de transclusion<article class="content__article">…</article> remplacera le<ng-content></ng-content> dans notre layout.
Simple, me direz-vous, mais imaginons avoir besoin de plusieurs blocs de contenu dynamique… C’est possible ! <ng-content> accepte un attribut select, qui nous permet de nommer un slot. Modifions notre layout pour accepter un 2nd slot.

*layout.component.html*
````
<section class="layout">
    <!-- slot header -->
    <nav class="layout__nav">
       <ng-content select="[cardNav]"></ng-content>
    </nav>
    <!-- slot content--> 
    <div class="layout__content">       
        <ng-content select="[cardContent]"></ng-content>
    </div>
</section>
````
	
Notez que l’on utilise select=[cardNav] && select=[cardContent]. Les “[]” veulent dire “à remplacer uniquement si l’élément possède l’attribut card-…”.
Et notre composant :
	
*articles.component.html*
````
<h1>Notre super App !</h1>
<app-layout>
    <!-- contenu dynamique : nav -->
    <a cardNav class="nav__cta">Article 1</a>
    <a cardNav class="nav__cta">Article 2</a>
    <a cardNav class="nav__cta">Article 3</a>        
    
    <!-- contenu dynamique : content -->
    <article cardContent class="content__article">
       <h2>Article 1</h2>
       <p>Mon super résumé...</p>
    </article> 
       
    <article cardContent class="content__article">
       <h2>Article 1</h2>
       <p>Mon super résumé...</p>
    </article>   
     
    <article cardContent class="content__article">
       <h2>Article 1</h2>
       <p>Mon super résumé...</p>
    </article>
<app-layout>
````

## Workspace
[Back to top](#angular)     

générer un workspace : ````ng new <mon-workspace> --create-application=false````
générer une librairie : ````ng g library <ma-lib>````
générer une application : ````ng g application <mon-ammplication>````
générer un composant dans un projet/lib du workspace (spécifier le projet/lib) : ````ng g c composant/mon-compo --project=<ma-lib>````

la création d'une application dans un workspace diffère de la création d'un projet classique dans le sens ou cette dernière n'a pas de package.json. Elle va utiliser le package.json du workspace. Ainsi en crééant plusieurs applications dans un même workspace, elles partageront toutes le même workspace.

Pour exposer un composant d'une librairie aux autres projets / lib, ajouter sa dépendance dans le fichier public.api.ts
//export * from './lib/composant/mon-composant';

Une librairie est en fait un projet angular dans lequel on peut déclarer des classes / services / composants que l'on va ensuite partager dans un **MEME** workspace. 
C'est utile si plusieurs projet doivent partager des composants / classes / services / helpers etc...

Si l'on souhaite utiliser une librairie dans des projets externes au workspace, il faut publier la librairie sur NPM privée ou publique (payant)

Si un projet du workspace souhaite rajouter des features à un composant / service / classe du workspace, il faut alors créer un nouveau composant / classe / service et le faire "extend" du composant / classe / service initial


**Liaison entre les applications et les librairies**

Afin de ne pas avoir à redéployer les librairies à chaque modification et permettre la mise à jour du code à chaud il faut configurer le fichier *tsconfig.json* du projet en définissant des redirections vers les chemins physique des fichiers. 

Par défaut ces redirections se font vers le répertoire "dist" du workspace. 
