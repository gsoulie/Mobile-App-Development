# Angular

## VSCode plugins

Angular schematics
Auto import
typescript hero => permet de créer des compos / pipe etc... en faisant un clic droit plutôt que la console
tslint / eslint

## Les 3 fichiers principaux pour créer une appli angular

main.ts permet de définir le type d'application (mobile, web, ...). Ensuite il appelle le module racine (AppModule)
app.module.ts
app.component.ts

## Best practices

### Pipe

Tout traitement qui modifie la vue doit préférablement utiliser les pipes plutôt qu'une méthode. Les pipes sont très optimisés et offrent un gain de performance énorme.

### Optimisation lancement application

1 - lazy loading
ne charger que les routes nécessaires au démarrage

2 - server side rendering
faire une capture de la page côté backend et l'envoyer au client, pendant ce temps là, angular charge le reste.
C'est juste une capture, le client ne peut pas intérragir. C'est juste en attendant.
cf : https://angular.io/guide/universal

### zone.js

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

## Spread & Rest operators

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

const user = [{nom: 'toto', prenom: 'paul'},{nom: 'titi', prenom: 'luc'}];
let [o1, o2] = user;


### Function parameters destructuration

maFunct = ({param1, param2}) {

}

maFunct({param2: 5, param1: 1});

==> permet de s'affranchir de l'ordre des paramètres et de gérer plus facilement les 
paramètres optionnels


## Angular project lifecycle

1 - main.ts
2 - app.module.ts => déclare tous les composants/directive/pipe/services de l'appli
3 - app.component.ts => c'est le bootstrap component

## Components interactions

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

codage en TS qui sera transpilé en JS car le navigateur ne sait pas interpreter le TS

## Web worker

Webworker permet de déleguer une tâche lourde (ex afficher un objet 3D calculé). Cela permet au thread principal, d'alléger sa mémoire
et de déléguer les tâches lourdes au webworker qui va s'en charger?


## injection de dépendance (services)

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

https://rxjs-dev.firebaseapp.com/guide/subject
https://makina-corpus.com/blog/metier/2017/premiers-pas-avec-rxjs-dans-angular

## Codes retour http

faire toujours une surcouche à httpclient voir APIHelper correction TP2

catch récupérer code erreur et le traiter dans ton service surcouche (retourner un enum) et interpréter
redirige l'erreur vers le composant concerné

## Form

**Template-driven** : la logique de validation du formulaire est dans la vue (C'EST MAL la vue ne doit faire QUE de la vue !)

**Model-driven-form** : la logique est dans le controller c'est la **bonne pratique** !!

Il utilise des FormGroup qui contiennent d'autres FormGroup ainsi que des FormControl. Le FormGroup permet de définir la logique pour tout un formulaire.
Le FormControl définit la logique d'un input du FormGroup

Pour faciliter l'écriture des formulaires, utiliser Angular FormBuilder : https://angular.io/guide/reactive-forms

### Custom validator
retourne null si tout va bien et retourne un objet en cas d'erreur

Un validator custom est une classe dans lequel on défini une methode statique.
=> this.champ = new FormControl(null, monvalidator.saMethodeStatique);

## Composants gratuits

codepen.io

