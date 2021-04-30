# Angular

[NOTIONS IMPORTANTES](https://github.com/gsoulie/angular-resources/blob/master/angular-summary.md)      

* [Ressources](#ressources)     
* [Notions avancées](#notions-avancees)      
* [VSCode plugins](#vscode-plugins)     
* [Généralités](#généralités)     
* [Commandes](#commandes)     
* [Update angular](#update-angular)     
* [ESLint](#eslint)       
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
* [Directives, ngClass, ngStyle](#directives)     
* [UI frameworks](#ui-frameworks)     
* [Theming](#theming)     
* [Adapter pattern](#adapter-pattern)     
* [Flex layout](#flex-layout)        
* [ng-template](#ng-template)     
* [ng-content](#ng-content)      
* [Workspace](#workspace)      
* [Debug avec vscode](#debug-avec-vscode)       
* [Variables d'environnement modifiables](#variables-d-environnement-modifiables)       
* [Test build prod en local](#test-build-prod-en-local)        
* [UI Components](#ui-components)      
* [mat-dialog template générique](https://github.com/gsoulie/angular-resources/blob/master/angular-dialog-template.md)        


## Ressources

https://alligator.io/angular/    
https://blog.thoughtram.io/    
https://nitayneeman.com/posts/all-talks-from-ng-conf-2018/    

## Notions avancées

[composant extend/collapse générique avec boucle de composants](https://makina-corpus.com/blog/metier/2019/des-boucles-generiques-de-composants-avec-angular)         
[content projection - attention ne fonctionne PAS avec les boucles](https://codecraft.tv/courses/angular/components/content-projection/)        

## VSCode plugins
[Back to top](#angular) 

* Angular Essentials (john papa)       
* Angular Language Service        
* Angular Snippets (v11 john papa)       
* Peacock (john papa)       
* Prettier Code formatter       
* Auto close tag       
* Auto Rename tag      
* Angular schematics    
* Auto import    
* Beautify (HookyQR)     
* Bookmarks (Alessandro Fragnagni)      
* Bracket Pair Colorizer      
* typescript hero => permet de créer des compos / pipe etc... en faisant un clic droit plutôt que la console    
* tslint / eslint    
* sass lint     
* Template String converter        

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
src
|
+ app
|  |
|  + components
|  |     |
|  |     + user
|  |     |  |
|  |     |  + user-list
|  |     |  |    |
|  |     |  |    + user-list.component.ts
|  |     |  |    + user-list.component.html
|  |     |  |    + user-list.component.scss
|  |     |  |    + user-list.component.spec.ts
|  |     |  |    
|  |     |  + user-detail
|  |     |  + ...
|  |     |  |
|  |     |  + shared
|  |     |  |   |
|  |     |  |   + user.service.ts
|  |     |  |   + user.service.spec.ts
|  |     |  |   + user.model.ts
|  |     |  |   + user.guard.ts
|  |     |  |   + ...
|  |     |  |
|  |     |  + user.module.ts
|  |     |  + user-routing.module.ts
|  |     |  
|  |     + ... 
|  |     
|  + shared     
|  |   |
|  |   + models
|  |   + pipes
|  |   + enum
|  |   + services
|  |   + guards
|  |   + interfaces
|  |
|  + app.module.ts
|  + app.component.ts
|  + app.component.html
|  + app.component.scss 
|  + app.component.spec.ts 
|  + material.module.ts
|  + app-routing.module.ts
|
+ maint.ts
+ index.html
+ style.scss
+ assets
|   |
|   + imgs
|   |  |
|   |  + icons
|   |  + ...
|   |  
|   + fonts
|
+ ...
 ````
 
### ngModel
[Back to top](#angular)   

| Name | Description |
| --- | --- |
| ngModel | Bind element to formControl | 
| [ngModel] | Simple-way binding (i.e. property binding) | 
| [(ngModel)] | Two-way binding | 

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

## ESLint
[Back to top](#angular) 

Depuis 2019, TSLint est déprécié, il est donc temps de basculer vers ESLint

[Ionic blog](https://ionicframework.com/blog/eslint-for-ionic-angular/)       

````
git add .
git commit -m "pre eslint"
git checkout -b feat-eslint

ng add @angular-eslint/schematics

// convert current tslint to eslint file
ng g @angular-eslint/schematics:convert-tslint-to-eslint {{YOUR_PROJECT_NAME_GOES_HERE}}

// once it's done you can run eslint and remove old tslint file and dependcies
rm tslint.json
npm uninstall tslint
````

## Best practices
[Back to top](#angular) 

### Model Adapter Pattern

Utiliser au maximum la technique du [adapter pattern](#adapter-pattern) pour gagner en maintenabilité

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
> Important : permet de s'affranchir de l'ordre des paramètres et de gérer plus facilement les 
paramètres optionnels

## Angular project lifecycle
[Back to top](#angular) 

1 - main.ts
2 - app.module.ts => déclare tous les composants/directive/pipe/services de l'appli
3 - app.component.ts => c'est le bootstrap component

## Components interactions
[Back to top](#angular) 

Angular fonctionne en single way data-binding, c'est à dire que les enfants ne peuvent communiquer qu'avec leur parent direct. C'est donc le parent qui transmet ses propriété via un *@Input*. Si l'enfant souhaite modifier une valeur, il doit en notifier son parent via un Event Emitter dans avec un *@Output*

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


> Important : l'enfant ne peut pas modifier l'objet fourni par le parent !
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
https://www.youtube.com/watch?v=TrDqaABq-UY&ab_channel=DevoxxFR         

on utilise les observables pour représenter l'arrivée de données synchrone ou asynchrone.

on peut recevoir une seule données ex : appel http
ou plusieurs données étalées dans le temps ex : websocket

l'observable a 3 type de notifications :

- next chaque arrivée d'une data
- error va casser l'observable, plus rien ne se passe
- complete est la terminaison, plus rien ne se passe

### opérateurs

**pipe** : opérateur principal qui va permettre le branchement de plusieurs autres opérateurs à la suite les uns des autres et ainsi travailler sur le flux de données
 
ex :
````
import {filter, map} from 'rxjs/operators;

getAlertMsg(): Observable<string> {
	const notif: Observable<Notification> = this.getNotifications();

   return notif.pipe(
	filter(notif => notif.type === 'ALERT'),
	map(notif => notif.code + ' : ' + notif.message)
   );
}
````

**filter**     
**every**      
**map**       
**reduce**      

> Important : les opérateurs appliqués **ne modifient jamais l'observable d'origine**, ils produisent une copie et renvoient un nouvel observable.


Pour pouvoir récupérer les données d'un observable, il faut s'y abonner via subscribe.

La souscription peut prendre 3 paramètres (next, error et complete) soit :
subscribe(value, error, ())
ou un objet de type observer
subscribe({value, error, ()})

> Important : Toujours penser à annuler les souscription !!

### 2 types d'observables 

- **cold (unicast)** = source démarrée pour chaque souscription. 10 souscriptions = 10 démarrage. recommence du début pour chaque utilisateur
ex appel http, redémarre à chaque appel

- **hot (multicasted)** = 1 seule source diffusé à tout le monde (toutes les souscriptions) simultanément. Si on arrive en cours de route on aura pas les données depuis le début.
ex données qui arrivent sur une websocket

> remarque : on peut transformer un cold en hot

### Création 
of(1, 2, 3); est un observable qui fait next(1); next(2); next(3); complete();

Création d'un hot observable
On va utiliser un Subject qui est à la fois un Observer et un hot Observable

````
const subject = new Subject<number>();
subject.subscribe(v => console.log('observerA : ' + v));
subject.next(1);
// observerA : 1
subject.subscribe(v => console.log('observerB : ' + v));
subject.next(2);
// observerA : 2
// observerB : 2
````

**behaviorSubject** : permet de conserver un état (valeur courante)

**ReplaySubject** : quand on souscrit on reçoit les dernières valeurs qui ont été mises en cache

**fromPromise(p)** : créer un observable à partir d'une promise
**toPromise()** : créer une promise à partir d'un observable
**fromEvent()** : créer un observable à partir d'un event (ex click bouton)

### Transformer un cold (ex : requête http) en hot

#### share() : partager un cold à tout un ensemble de souscripteurs
````
// attention exécution se fait à la première souscription. Si on souscrit et que la réponse est déjà arrivée on aura rien
const hot$ = cold$.pipe(share());
````

#### shareReplay(5) 

> Important notion NR. Voir rubrique exemple plus bas

````
const hot$ = cold$.pipe(shareReplay(1));
// si la réponse été déjà passée, au moment de la souscription on reçoit immédiatement la réponse (il rejoue le dernier résultat à chaque nouvelle souscription)
// remarque, ne rejoue PAS la requête
````

### Observable imbriqués 

#### Aplatir 

|action|opération|opérateur unique|
|-|-|-|
|exécution parallèle|map(), mergeAll()|mergeMap()|
|exécuter à la suite|map(), concatAll()|concatMap()|
|annuler la précédente|map(), switch()|switchMap()|
|annuler la nouvelle|map(), exhaust()|exhaustMap()|

**switchMap** utilisé dans le cas d'une complétion automatique. On veut les résultat de la dernière requête (ce que l'utilisateur a tappé en dernier)
=> A chaque nouvelle frappe on annule la requête précédente

**exhaustMap** : tant que le traitement en cours n'est pas terminé on ne tient pas compte des traitements suivants

### Bonnes pratiques

#### Services asynchrones 

Quand on fait un service qui retourne un observable, **on ne souscrit JAMAIS à l'observable dans le service** pour renvoyer les données directement,
car on ne sait pas quand les données arriveront

#### Erreurs

Remonter les erreurs là où on peut les traiter.

interception : catchError
rééssayer : retry ou retryWhen

ex : 

````
find(id: string): Observable<Resource> {
	const url = `http://.../.../${id}`;
	return this.httpClient.get<Resource>(url)
	.pipe(
		catchError(error => {
			if (error && error.status === 404) {
				return of(null);
			}
			throw error;
		});
		);
}
````

### Exemples

#### cold to hot observable
On veut créer une liste de livres qui ne va pas souvent être mise à jour, on utilise une requête http (cold donc)
pour renseigner la liste. Le soucis c'est que pour chaque souscription, on va rejouer la requête.

Si on ne veut pas que cela se produise, on va convertir le cold en hot observable

*1 requête http*
````
list$: Observable<Book[]>;

constructor(private httpClient: HttpClient) {
	this.list$ = this.buildRequestObservable();
}

buildRequestObservable() {
	return this.httpClient
	.get<Book[]>(url, {param: params})
	.pipe(
		shareReplay(1);
		);
}

getList(): Observable<Book[]> {
	return this.list$;
}
````

Si on souhaite maintenant rafraichir nos data toutes les heures (uniquement si il y a une nouvelle souscription), il suffira d'ajouter un interval 

*1 requête http max / 1h*
````
constructor(private httpClient: HttpClient) {
	this.list$ = this.buildRequestObservable();
	setInterval(() => {
		this.list$ = this.buildRequestObservable(),
	}, 3600 * 1000);
}
...

````

#### auto-complete de recherche

````
this.countryList$ = this.countryControl.valueChanges
.pipe(
	map(name => name.trim()),
	filter(name => length >= 2), // filtrer uniquement si au moins 2 caractères
	debounceTime(200), //attente 200ms après dernière valeur, avant envoi requête
	distinctUntilChanged(), // filtrer uniquement si valeur différente de la valeur précédente
	switchMap(name => this.countryService.search(name))
	);


search(name: string): Observable<string[]> {
	name = name && name.trim();
	if (name) {
		const url = 'https://.......';
		return this.httpClient.get<Country[]>(url + name)
		.pipe(
		map(countries => countries.map(country => country.translations.fr)),
		catchError(error => of([]))
		);
	}
	return of([]);
}
````

## RxJs 
[Back to top](#angular) 

https://rxjs-dev.firebaseapp.com/guide/subject       
https://makina-corpus.com/blog/metier/2017/premiers-pas-avec-rxjs-dans-angular       

### opérateurs

|operator|description|
|-|-|
|pipe|permet le chaînage de plusieurs opérateurs|
|map|L'opérateur map permet de créer un nouvel Observable à partir de l'Observable d'origine en transformant simplement chacune de ses valeurs.|
|tap|obsolète|

## Codes retour http
[Back to top](#angular) 

Il est conseillé de toujours faire un service qui surcharge httpClient (voir apiHelper).

On peut ensuite l'améliorer en ajoutant un catch en cas d'erreur qui permet de récupérer le code erreur et le traiter dans le helper (retourner un enum) et rediriger l'erreur vers le composant concerné.

## Form
[Back to top](#angular) 

**Template-driven** : la logique de validation du formulaire est dans la vue (C'EST MAL la vue ne doit faire QUE de la vue !)

**Model-driven-form** : la logique est dans le controller c'est la **bonne pratique** !!

Il utilise des FormGroup qui contiennent d'autres FormGroup ainsi que des FormControl. Le FormGroup permet de définir la logique pour tout un formulaire.
Le FormControl définit la logique d'un input du FormGroup

Pour faciliter l'écriture des formulaires, utiliser Angular FormBuilder : https://angular.io/guide/reactive-forms


### Générateur de formulaires

Générateur automatique de formulaires : http://zerocodeform.com/

### FormBuilder

Permet de simplifier l'écriture des formulaires ReactiveForm

*vue.html*
````
<form [formGroup]="loginForm" novalidate (ngSubmit)="onSubmit()">
    
    <div>
        <label>Login</label>
        <input type="text" formControlName="login" placeholder="">
    </div>
    <div>
        <label>Password</label>
        <input type="password" formControlName="password" placeholder="">
    </div>
    
    <button type="submit">Submit</button>
</form>
````

*controller.ts*
````
loginForm: FormGroup;

// Méthode avec FormBuilder
constructor (private fb: FormBuilder) { }

ngOnInit() {
	this.loginForm = this.fb.group({
		login: [isDevMode() ? 'admin' : '', Validators.required],
		password: [isDevMode() ? 'password' : '', Validators.required]
	});
	
	// Méthode sans FormBuilder

	this.loginForm = new FormGroup({
		login: new FormControl('admin', Validators.required),
		password: new FormControl('password', Validators.required)
	});
}

onSubmit() {
   console.log(this.fb.value.login);
   console.log(this.fb.value.password);
}
````

**Remarque** : penser à importer le module *ReactiveFormsModule* dans le *app.module.ts*

> Exemple complet : https://github.com/gsoulie/angular-resources/blob/master/angular-forms.md#reactive-form

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

> A savoir : *href* recharge la page, pas le *routerLink*

### Exemple de routing avec children

````
const ROUTES: Routes = [
	{ path: 'user', children: [
		{ path: '', component: UserListComponent },
		{ path: 'edit/:id', component: UserEditComponent },
		{ path: 'add', component: UserAddComponent },
		{ path: 'delete/:id', component: UserDeleteComponent },
		{ path: ':id', component: UserComponent }	// ATTENTION à mettre en dernier sinon elle interceptera tous les autres routes
	]},
	{ path: '**', component: ErrorComponent }
]
````

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
		component: HomeComponent,	// si on souhaite toujours afficher le composant Home en plus de ses enfants
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

Exemple complet d'un routing via un tagGroup (onglet) avec retour sur le parent depuis une modale enfant. 

Cas d'utilisation : Une page principale contient un tab *home-tabs* contenant 3  onglets (home, queries, lists). Depuis les onglets *queries* et *lists* on a un bouton qui ouvre une modale *results*. A la fermeture de la modale on souhaite revenir sur le tab principal

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

Naviguer vers la modale *results*

````
// Navigating from queries page 
<ion-item tappable routerLink="results/{{ item.queryId }}" routerDirection="forward">

// Navigating from lists page
<ion-button routerLink="results">results</ion-button>
````

Revenir sur l'onglet parent courant depuis la modale

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

Les directives permettent de modifier les éléments du DOM. **Leur responsabilité est relative à la vue**

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

### ngClass
[Back to top](#angular)    

Selon le contexte, si un traitement conditionnel est utilisé plusieurs fois dans l'appli et/ou avec de l'algo à faire, utiliser une directive.

Si c'est un cas très ponctuel, utiliser ````[ngClass]````

````<label [ngClass]="{'myCssClass': i > 5 ? true : false}">my content</label>````

### ngStyle

````
<p [ngStyle]="{backgroundColor: getColor()}"></p>

<label [ngStyle]="{'background-color':myVar < 5 ? 'blue' : 'green'}">my content</label>
````

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

````ng add @angular/material````

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

### Bootstrap
[Back to top](#angular)   

Installation : ```npm install --save bootstrap```, ensuite ajouter la configuration dans le **angular.json** sous la rubrique ```architect/build/styles``` :

```
"styles": [
    "node_modules/bootstrap/dist/css/bootstrap.min.css",
    "src/styles.css"
]

```

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

### Global sass variables

Regrouper les variables sass dans le fichier *src/variables.scss*

*variables.scss*

````
:root
{
  --darkgrey: #23272D;
  --mediumgrey: #3F464B;
  --mediumgrey2: #5B6164;
  --lightgrey: #ECEDED;
  --labelgrey: #D9D9D9;
  --yellow: #FFD400;
  --lightblue: #75C4D5;
  --mediumblue: #009CBE;
  --green: #70B62C;
}
````

Il suffit ensuite d'injecter le fichier variable.scss dans le *angular.json* 

````
...
"styles": [
              {"input":"src/variables.scss"}
            ],
````

*component.scss file*

````
.container {
  background-color: var(--mediumgrey);
}
````

## Adapter pattern
[Back to top](#angular)      
Le Model Adapter Pattern permet de simplifier le code des retours d'observable et aussi de respecter la pratique du DRY (Don't repeat yourself)

https://florimond.dev/blog/articles/2018/09/consuming-apis-in-angular-the-model-adapter-pattern/

Le but est de simplifier le code suivant : 

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

En utilisant un Adapter : 


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

Ceci permet de rendre le code plus adaptable si le backend venait à être modifié (ex : renommage d'un paramètre, changement de type etc...)

Ex : Côté backend on renomme le paramètre "name" par "label". Il y a juste à modifier l'adapter sans changer la classe initiale sans rien changer d'autre dans le code.

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

*app.component.html*

````
<mat-toolbar color="primary">
    <span>Card view demo</span>
    <div fxHide.lt-md>
      <span class="column-label">Columns</span>
      <mat-slider [max]="6" [min]="3" [(ngModel)]="gridColumns" [thumbLabel]="true">
      </mat-slider>
    </div>
  </mat-toolbar>
<div class="content">
    <div fxLayout="row wrap" fxLayoutGap="16px grid">
        <div [fxFlex]="(100/gridColumns) + '%'" fxFlex.xs="100%" fxFlex.sm="33%" *ngFor="let num of [1,2,3,4,5,6,7]">
        
        <!-- Utiliser le redimenssionnement classique sans le slider -->
            <!-- <div fxFlex="25%" fxFlex.xs="100%" fxFlex.sm="33%" *ngFor="let num of [1,2,3,4,5,6,7]"> -->
            <mat-card class="mat-elevation-z4" appCardBorder>
            <mat-card-header>
                <mat-card-title>Himalayan Peaks</mat-card-title>
            </mat-card-header>
            <img mat-card-image src="./../assets/images/2-chtulhu.jpg">
            <mat-card-content>
                <p>
                The Himalayas is a mountain range in Asia.
                </p>
            </mat-card-content>
            <mat-card-actions>
                <button mat-button>LIKE</button>
                <button mat-button>SHARE</button>
            </mat-card-actions>
            </mat-card>
        </div>
    </div>
  </div>
````

*app.component.scss*

````
.flex-container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
}
.box {
    min-width: 200px;
    height: 180px;
    padding: 50px;
    font-size: 22px;
}
.content {
    padding: 16px;
}

.content > mat-card {
    width: 200px;
}

mat-toolbar {
    justify-content: space-between;
}
.content > mat-card {
    margin-bottom: 16px;
}

.column-label {
    margin-right: 8px;
    font-size: 1rem;
}
````
## ng-template
[Back to top](#angular)

https://blog.angular-university.io/angular-ng-template-ng-container-ngtemplateoutlet/

*ng-template* défini un template qui n'affiche rien tant qu'il n'est pas utilisé

````
<div class="lessons-list" *ngIf="lessons else loading">
  ... 
</div>

<!-- Ne sera affiché uniquement dans le cas else -->
<ng-template #loading>
    <div>Loading...</div>
</ng-template>
````

Il n'est pas possible d'appliquer plusieurs directives à un même élément, par exemple un *ngIf* et *ngFor* sur un même conteneur.
Pour palier ce problème, on peut créer une div pour le *ngIf* et une div pour le *ngFor*. Cela fonctionne mais oblige à créer une nouvelle div.

Il est donc possible d'utiliser un *ng-container*

Le ng-container permet en outre l'injection dynamique d'un template dans une page, un placeholder en quelques sortes

````
<ng-container *ngTemplateOutlet="loading"></ng-container>

<ng-template #loading>
    <div>Loading...</div>
</ng-template>
````

Il est possible de passer un template à un composant enfant :

*parent*
````
    <ng-template #testTemplate let-clientVar="client">
        <div class="customTemplate">
            <h1>Hello {{ clientVar }} !</h1>
            <p>This is my custom template</p>
        </div>
    </ng-template>
    
    <app-generic-collapsible-list [itemTemplate]="testTemplate"></app-generic-collapsible-list>
````

*enfant app-generic-collapsible-list*
````
<ng-template #defaultTabButtons>
    <div class="default-tab-buttons">
        ...
    </div>
</ng-template>

<ng-container *ngTemplateOutlet="itemTemplate ? itemTemplate: defaultTabButtons">
</ng-container>
````

*enfant controller*
````
@Input() itemTemplate: TemplateRef<any>;
````

### Variable contexte

#### Exemple 1

Les ng-template peuvent prendre des paramètres. Ici le paramètre *when* contient une valeur comme "morning", "afternoon" ou "evening" :

````
<ng-template #hello let-when="whenValue">
  Good {{ when }} !
</ng-template>
````
*let-xxx* permet de définir des variables utilisables dans le ng-template (ici when) à partir de la propriété (ici whenValue) d'un objet passé en "context" du *ngTemplateOutlet*. Ces variables ne sont pas accessible depuis l'extérieur directement. Pour accéder à ces variables depuis le ng-container, il faut créer un contexte (objet json par exemple) qui a un attribut
ayant le nom de la variable à toucher :

````
<ng-container *ngTemplateOutlet="itemTemplate;context:{whenValue: 'morning'}">
</ng-container>
````

#### Exemple 2
````
<ng-template #testTemplate let-clientVar="client">
    <div class="customTemplate">
        <h1>Hello {{ clientVar }} !</h1>
        <p>This is my custom template</p>
    </div>
</ng-template>

<ng-container *ngTemplateOutlet="testTemplate;context:ctx"></ng-container>
````

*controller*
````
client = "gsoulie";
ctx = {client: this.client};
````

### Accéder au contexte depuis un composant enfant 

*View*

````
<div *ngFor="let num of [1,2,3,4,5,6,7]">
    <ng-container *ngTemplateOutlet="itemTemplate;context:{client:num}">
    </ng-container>
</div>
````

*Controller*
````
@Input() itemTemplate: TemplateRef<{client:any}>;
````

### boucles génériques de composant extand/collapse

ATTENTION : ne fonctionne pas avec un jeu de données qui vient d'un observable

https://makina-corpus.com/blog/metier/2019/des-boucles-generiques-de-composants-avec-angular

## ng-content
[Back to top](#angular)

https://wizbii.tech/un-layout-dynamique-avec-ng-content-d00e27ab26d9      
https://github.com/gsoulie/angular-resources/blob/master/angular-summary.md#ng-content    

La balise ````<ng-content>```` permet de définir un modèle de vue fixe et de définir un emplacement pour du contenu dynamique.
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
	
Le slot de transclusion ````<article class="content__article">…</article>```` remplacera le ````<ng-content></ng-content>```` dans notre layout.
Imaginons avoir besoin de plusieurs blocs de contenu dynamique… C’est possible ! ````<ng-content>```` accepte un attribut ````select````, qui nous permet de nommer un slot. Modifions notre layout pour accepter un 2nd slot.

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
	
Notez que l’on utilise ````select=[cardNav] && select=[cardContent]````. Les "[]" veulent dire "à remplacer uniquement si l'élément possède l'attribut *card-…*".
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
       <h2>Article 2</h2>
       <p>Mon super résumé...</p>
    </article>   
     
    <article cardContent class="content__article">
       <h2>Article 3</h2>
       <p>Mon super résumé...</p>
    </article>
<app-layout>
````

## Workspace
[Back to top](#angular)     

Un workspace Angular est ensemble d'application et de librairies. Toutes les applications d'un même workspace partageront les mêmes dépendances (angular.json / package.json)

générer un workspace : ````ng new <mon-workspace> --create-application=false````      
générer une librairie : ````ng g library <ma-lib>````       
générer une application : ````ng g application <mon-application>````       
générer un composant dans un projet/lib du workspace (spécifier le projet/lib) : ````ng g c composant/mon-compo --project=<ma-lib>````

Si on ne spécifie pas dans quel projet / lib on souhaite générer un composant, ce dernier sera généré dans la cible par défaut spécifiée dans le angular.json sous la clé "defaultProject"

la création d'une application dans un workspace diffère de la création d'un projet classique dans le sens ou cette dernière n'a pas de package.json. Elle va utiliser le package.json du workspace. Ainsi en crééant plusieurs applications dans un même workspace, elles partageront toutes le même workspace.

Une librairie est en fait un projet angular dans lequel on peut déclarer des classes / services / composants que l'on va ensuite partager dans un **MEME** workspace. 
C'est utile si plusieurs projet doivent partager des composants / classes / services / helpers etc...

Si l'on souhaite utiliser une librairie dans des projets externes au workspace, il faut publier la librairie sur NPM privée ou publique (payant)

### Exposer un composant aux autres libs / projets

Comme pour un projet angular classique, lors de la création d'un composant, service etc... dans la lib, vérifier que sa dépendance est ajoutée dans le noeud *exports* du fichier module.ts associé. 
Ensuite il faut ajouter sa dépendance dans le fichier *public.api.ts*       

````
//export * from './lib/composant/mon-composant';
ex : export * from './lib/componants/demo-composant/demo-composant.component';
````

Ensuite il faut faire un build de la lib : ````ng build lib-demo````

Les composants / services etc... de la lib sont maintenant accessibles à toutes les applications du workspace à condition de penser à ajouter l'import du module de la lib concernée dans le *app.module.ts* de chaque application.

### Etendre un composant / classe

Si un projet du workspace souhaite rajouter des features à un composant / service / classe du workspace, il faut alors créer un nouveau composant / classe / service et le faire "extend" du composant / classe / service initial

**Liaison entre les applications et les librairies**

> Remarque : la modification d'un élément d'une lib n'est pas répercuté à chaud dans les applications en cours d'exécution. Il faut obligatoirement recompiler la lib puis relancer les applications pour voir apparaître les modifications.

Afin de ne pas avoir à redéployer les librairies à chaque modification et permettre la mise à jour du code à chaud il faut configurer le fichier *tsconfig.json* du projet en définissant des redirections vers les chemins physique des fichiers. 

Par défaut ces redirections se font vers le répertoire "dist" du workspace. 

## Debug avec vscode
[Back to top](#angular)   

- 1 : Installer l'extension vscode debugger for chrome
- 2 : Dans l'onglet debug, créer une nouvelle configuration. Ceci va créer un répertoire .vscode contenant un fichier *launch.json*

````
{
    "version": "0.2.0",
    "configurations": [
       "name": "launch ng serve and chrome",
            "type": "chrome",
            "request": "launch",
            "preLaunchTask": "npm: start",
            "url": "http://localhost:4200/",
            "webRoot": "${workspaceFolder}",
            "sourceMaps": true,
            "sourceMapPathOverrides": {
                "webpack:/*": "${webRoot}/*",
                "/./*": "${webRoot}/*",
                "/src/*": "${webRoot}/*",
                "/*": "*",
                "/./~/*": "${webRoot}/node_modules/*"
              }
    ]
}
````

- 3 : créer une nouvelle task dans le fichier *task.json*

````
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "npm",
			"script": "start",
			"isBackground": true,
			"presentation": {
				"focus": false,
				"panel": "dedicated",
				"showReuseMessage": true,
				"clear": false
			},
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"problemMatcher": [],
			"label": "npm: start",
			"detail": "ng serve --open",
			"options": {
				"cwd": "${workspaceFolder}"
			}
		}
	]
}
````

- 4 : placer des points d'arrêts dans le code
- 5 : aller dans l'onglet debug et exécuter le fichier *launch.json* voulu (important : il est possible qu'il faille le lancer 2 fois)

Depuis le volet debug on a alors accès aux variables du scope dans le volet *variables* et il est possible d'ajouter des variables spécifiques à surveiller en les ajoutant dans l'onglet *watch*

> remarque : il est possible d'éditer un point d'arrêt pour lui dire de se déclencher sur une valeur précise par exemple

## Variables d'environnement modifiables
[Back to top](#angular)   

Dans certains cas il est nécessaire de pouvoir changer certaines variables d'environnement après compilation (ex : déploiement multi-sites, multi-environnements etc...)

Angular met à disposition un répertoire *environnements* contenant les fichiers *environment.prod.ts* et *environment.ts*. Ces fichier sont pratiques dans le cas du déploiement d'une application simple, sur un environnement unique. Mais pose quelques problèmes dans le cas d'un déploiement plus complexe. 
En effet les fichiers du répertoire *environments* sont compilés lors du build et ne sont alors plus accessibles ce qui pose problème si l'on souhaite pouvoir modifier certaines variables après compilation.

Pour pallier ce problème, il existe plusieurs solutions. Dans tous les cas, la première étape consiste à créer un fichier json qui contiendra les variables d'environnement et qui sera placé dans le répertoire *assets* ou dans un autre répertoire au même niveau. 

> En effet, les fichiers présents dans le répertoire *assets* restent accessibles et modifiables après compilation.

Par exemple :

*assets/env/settings.json*
````
{
    "AppSettings": {
		"Environment": "Develop"
        "url": "url-de-prod",
        "api": "https://api-prod"
    }, 
	"Logging": {
		"LogLevel": {
			"Default": "Warning"
		}
	},
	"AllowedHosts": "*"
}
````

### Solution 1 : Utilisation des assets avec HttpClient

Ensuite la lecture peut se faire au lancement de l'application via un httpClient

> ATTENTION : version non optimisée, en effet il est préférable d'injecter le service qui lit les données dans une factory appellée dans le APP_INITIALIZER (voir solution 2)

*app.component.ts*

````
import { Subscription } from 'rxjs';
import { DataService } from './services/data.service';
import { Component, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnDestroy {
  
  settingsObservable: Subscription;

  constructor(private dataService: DataService) {
    // read settings
    this.settingsObservable = this.dataService.getAppSettings()
    .subscribe(res => {
      console.log(res);
    })
  }

  ngOnDestroy() {
    this.settingsObservable.unsubscribe();
  }
}

````

*data-service.ts*

````
export class DataService {
  private _appSettingsUrl = 'assets/env/settings.json';

  constructor(private http: HttpClient) { }
  
  //lire les settings json
  getAppSettings(): Observable<any> {
    return this.http.get(this._appSettingsUrl);
  }
}
````

### APP_INITIALIZER 

APP_INITIALIZE est un type multi-provider qui permet de spécifier une factory qui retourne une promise. Quand la promise est *complete* l'application continue son exécution. Ainsi, lorsqu'on arrive à l'endroit du code code où nous avons besoin des informations de configuration, on est certain qu'elles ont été chargées.

import { APP_INITIALIZER } from '@angular/core'

@NgModule({
    ....
    providers: [
        ...
        {
            provide: APP_INITIALIZER,
            useFactory: load,
            multi: true
        }
    ]
)
*load* est une fonction qui retourne une fonction qui retourne une **Promise**. La fonction Promise charge les informations de configuration et les enregistre dans l'application. Une fois que les infos de configuration ont été chargées, il faut resolve la promise **resolve(true)**.

Dernier point vraiment **important**, sans ça le code n'attendra pas d'avoir terminé avant de continuer, *useFactory* **DOIT** pointer vers une fonction qui pointe sur une **Promise**

*multi* : true est appliqué car APP_INITIALIZER autorise plusieurs instances de ce provider. Toutes les instances sont exécutées simultanément mais le code ne continuera pas tant que toutes les instances (Promises) ne sont pas terminées.

### Solution 2 : Utilisation d'une factory dans le APP_INITIALIZER app.module.ts
[Back to top](#angular)   

https://www.prestonlamb.com/blog/loading-app-config-in-app-initializer

#### exemple perso

*interfaces*
````
export interface IEnvironmentVariable {
    AppSettings: IAppSettings
}
export interface IAppSettings {
    site: string,
    url: string,
    tracelog: boolean,
    api: string
}
````

*app.module.ts*

````
import { AppconfigService } from './shared/services/appconfig.service';
import { BrowserModule } from '@angular/platform-browser';
import { APP_INITIALIZER, NgModule } from '@angular/core';
...

export function initConfig(appConfigService: AppconfigService) {
  return () => appConfigService.loadConfig();
}

@NgModule({
  declarations: [
    AppComponent,
    ...
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    ...
  ],
  providers: [{
		provide: APP_INITIALIZER,
		useFactory: initConfig,
		deps: [ AppconfigService ],
		multi: true
	}],
  bootstrap: [AppComponent]
})
export class AppModule { }
````

*AppConfigService.ts*
````
import { IEnvironmentVariable } from './../models/config.interface';
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class AppconfigService {
  private _config: IEnvironmentVariable;
  configSubject$;

  public get config(): IEnvironmentVariable {
    return this._config;
  }
  public set config(value: IEnvironmentVariable) {
    this._config = value;
  }
  
  constructor(private _http: HttpClient) {}

  public loadConfig() {
      
      return this._http.get('assets/env/settings.json')
          .toPromise()
          .then((config: IEnvironmentVariable) => {
              this.config = config;
              return this.config;
              //this.configSubject$.next(this.config);	// error  
          })
          .catch((err: any) => {
              console.error(err);
          });
  }
}
````

*app.component.ts*
````
  env: IEnvironmentVariable;
  settings: IAppSettings;

  constructor(private appconfigService: AppconfigService) { }
  
  ngOnInit() {
    this.env = this.appconfigService.config;
    this.settings = this.env.AppSettings;
  }
````


#### Exemple complexe
[Back to top](#angular)   

*exemple*

````
import { Config } from 'projects/Apps/Example/src/configs/config';
import { ApisConfig, ApisConfigurationProvider, ApisServicesModule } from 'apis-helpers';
import { UncatchedErrorHandler } from 'angular-helpers';

/**
 * Use to update config of library after loaded in APP_INITIALIZER
 */
@Injectable({ providedIn: 'root' })
export class ConfigFromApp extends ApisConfigurationProvider {
  constructor(private configStore: Config) {
    super();
    console.log('Load application configuration');
  }

  get params(): ApisConfig {
    return this.configStore.params;
  }
}

@NgModule({
  imports: [
    BrowserModule,
    AppRoutingModule,
    ApisServicesModule.forRoot({
      config: {
        provide: ApisConfigurationProvider,
        useClass: ConfigFromApp
      }
    })
  ],
  declarations: [
    AppComponent
  ],
  schemas: [ CUSTOM_ELEMENTS_SCHEMA ],
  providers: [
    {
      provide: LoggerConfig,
      useFactory: resolveNgxLoggerConfig
    },
    {
      provide: APP_INITIALIZER,
      useFactory: (configService: Config) => () => configService.loadConfig(),
      deps: [Config], multi: true
    },
    { provide: ErrorHandler, useClass: UncatchedErrorHandler }
  ],
  bootstrap: [AppComponent]
})
export class AppModule {}

export function resolveNgxLoggerConfig(): LoggerConfig {
  const suffix = Config.getApiSuffix(Config.params.logsApi);
  const config = {
    serverLoggingUrl: (Config.params ? Config.params.logsApi + suffix + '/logs' : undefined),
    level: NgxLoggerLevel.DEBUG,
    serverLogLevel: NgxLoggerLevel.INFO
  };
  return config;
}
````

*config.ts*
````
import { Injectable } from '@angular/core';
import configForTest from './config.json';
import configEnvForTest from './config.test.json';
import { ConfigService } from 'angular-helpers';
import { ApisConfigurationInterface } from 'apis-helpers';

@Injectable({ providedIn: 'root' })
export class Config extends ConfigService {

  static params: ApisConfigurationInterface;
  public params: ApisConfigurationInterface;
  public paramsPromise: Promise<ApisConfigurationInterface>;

  configUrl = 'configs/config.json';
  configEnvUrl = 'configs/config.env.json';

  static loadConfigForTest() {
    ConfigService.params = Object.assign({}, configForTest, configEnvForTest);
  }

  static apiUseGateway(api: string): boolean {
    return api.startsWith(this.params.gatewayApi);
  }

  static getApiSuffix(api: string): string {
    return this.apiUseGateway(api) ? '' : '/api';
  }

  static getHubSuffix(api: string): string {
    return this.apiUseGateway(api) ? 'Hub' : '';
  }

  static loadConfig(callback: (config: ApisConfigurationInterface) => void) {
    super.loadConfig(callback);
  }

  public loadConfig(): Promise<ApisConfigurationInterface> {
    return <Promise<ApisConfigurationInterface>> super.loadConfig();
  }
}
````

## Test build prod en local
[Back to top](#angular)   

Procédure pour pouvoir tester le résultat du *build --prod* en local sur la machine :

````
npm install http-server -g	// installer le serveur http en local
http-server dist/your-project-name // se placer dans le répertoire de l'application pour démarrer le serveur http
// ouvrir un navigateur et aller sur http://localhost:8080/
````

Il est maintenant possible de modifier le fichier json de configuration présent dans le répertoire *assets* et faire un ctrl-f5 pour voir la modification des variables.

## UI Components
[Back to top](#angular)        

https://github.com/gsoulie/angular-resources/blob/master/angular-component.md#components 
