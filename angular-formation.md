# Angular

* [Ressources](#ressources)     
* [VSCode plugins](#vscode-plugins)     
* [Généralités](#généralités)     
* [Update angular](#update-angular)     
* [Best practices](#best-practices)     
* [Spread & Rest operators](#spread-&-res-operators)     
* [Object destructuration](#object-destructuration)     
* [Angular project lifecycle](#angular-project-lifecycle)     
* [Components interactions](#components-interactions)     
* [Directive structurelle](#directive-structurelle)     
* [Typescript](#typescript)     
* [Web worker](#web-worker)     
* [injection de dépendance (services)](#)     
* [Promise](#promise)     
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


## Ressources

https://alligator.io/angular/    
https://blog.thoughtram.io/    
https://nitayneeman.com/posts/all-talks-from-ng-conf-2018/    


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

### Commandes

Créer un composant

````
ng g c components/home --module app
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

## Best practices
[Back to top](#angular) 

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

**Parent **

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
````

### Routing parameters
[Back to top](#angular) 

````
{
	path: 'ticket/edit/:id'
	component: TicketComponent
}
````

````

````

### Naviguer depuis le controller
[Back to top](#angular) 

````
this.route.nagivate(['./ticket', 'edit', idTicket], {relativeTo: this.asctivatedRoute});	// => /ticket/edit/12
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

## Theming
[Back to top](#angular)   

[Documentation](https://material.angular.io/guide/theming)     

Créer un fichier src/mon-theme**.scss** contenant la structure suivante :

````
@import '~@angular/material/theming';
@include mat-core();

// $my-app-primary: mat-palette($mat-blue-grey);
// $my-app-accent:  mat-palette($mat-pink, 500, 900, A100);
// $my-app-warn:    mat-palette($mat-deep-orange);
// $my-app-theme: mat-light-theme($my-app-primary, $my-app-accent, $my-app-warn);
// @include angular-material-theme($my-app-theme);

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
