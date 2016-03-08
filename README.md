# ionic start guide

##Introduction

ionic est un SDK HTML5 permettant de développer des applications mobiles hybrides basées sur les tehncologies HTML5, CSS, javascript.

##Installation

###Atom

#####1 - Installer Atom

#####2 - Installer les commandes shell 

Ouvrir Atom et depuis le menu principal faire Install shell command (ceci permet d’utiliser la commande apm pour installer des package sous Atom)

#####3 - Configurer la MAJ automatique d’Atom

Dans un terminal, saisissez la ligne :

```$ apm install auto-update-packages```

Redémarrez ensuite Atom

#####4 - Installation de packages utiles

```$ apm install atom-typescript```

```$ apm install ionic-atom```

```$ apm install atom-beautify```

###Ionic Framework

Installer le framework ionic via la ligne de commande 

```$ npm install -g cordova ionic```

###Cordova
####Installer cordova 

```$ sudo npm install -g cordova```

####Configuration des variables d’environement

```nano ~/.bash_profile```

Puis ajouter dans le fichier bash : 

```export ANDROID_HOME=/Users/gsoulie/Library/android-sdk-macosx
export PATH=${PATH}:/Users/gsoulie/Library/android-sdk-macosx/tools:/Users/gsoulie/Library/android-sdk-macosx/platform-tools```

###Gulp

Pour pouvoir surcharger les styles et utiliser les thèmes tels que Material design, il est nécessaire d’installer le package gulp

```$ sudo npm install -g gulp```

###Package geolocation

```$ cordova plugin add org.apache.cordova.geolocation```

###Package camera

```$ cordova plugin add org.apache.cordova.camera```

###Bower

```sudo npm install -g bower```





##Best practices

(https://github.com/johnpapa/angular-styleguide)
(https://github.com/toddmotto/angular-styleguide)



##Ressources

(http://www.sitepoint.com/building-simple-app-using-ionic-advanced-html5-mobile-app-framework/)
(http://www.sitepoint.com/5-ionic-app-development-tips-tricks/)
(http://ngcordova.com/)

###ionic creator

Est une application web permettant de construire les views ionic via drag and drop. C’est une application libre d’utilisation. On peut ensuite importer les views dans son projet.

##Démarrage

###Création d’un nouveau projet 

```$ ionic start myApp blank```

#####Configurer les plateformes

```$ cd myApp```

Attention, à jouer les commandes suivantes dans le répertoire du projet :
(http://ionicframework.com/docs/guide/testing.html)

```$ ionic platform add ios (ou android)```

```$ ionic build android```

#####Tester l’application
######Sur émulateur

```$ ionic emulate android``` 

######Sur navigateur

```$ ionic serve```

######Sur device

```$ ionic run android```

###Architecture d’une application ionic

**View** < Template < **Controller** < {data} < **Service**

```<div>[{data}]</div>``` < Template < ```$scope = {data}``` < {data} < ```Return {data}```

###Structure générale d’un projet ionic
```
├── hooks          // custom cordova hooks to execute on specific commands
├── platforms      // iOS/Android specific builds will reside here
├── plugins        // where your cordova/ionic plugins will be installed
├── resources        // icon and splash screen
├── scss           // scss code, which will output to www/css/
|── www         // application - JS code and libs, CSS, images, etc.
     |---------css                 //customs styles
     |---------img               //app images
     |---------js                  //angular app and custom JS
     |---------lib                //third party libraries
     |---------index.html  //app master page        
├── bower.json     // bower dependencies
├── config.xml     // cordova configuration
├── gulpfile.js    // gulp tasks
├── ionic.project  // ionic configuration
├── package.json   // node dependencies
```

###Structurer un projet

(https://blog.nraboy.com/2015/03/create-todo-list-mobile-app-using-ionic-framework/)

###Déclaration des pages dans app.js

Pour une meilleur organisation, il est conseillé de créer un répertoire /www/templates dans lequel seront créées les différents pages html de l’application.

Ces pages doivent ensuite être déclarées dans le fichier app.js de l’application afin de pouvoir les utiliser. On utilise alors la syntaxe suivante :

```
.config(function($stateProvider){
	$stateProvider

	.state('main', {
		url: "/main",
		templateUrl: "templates/main.html",
		controller: 'MainCtrl'
	});
$urlRouterProvider.otherwise('/main');
});
```

Le fichier ```app.js``` permet de définir la structure de l’application dans la directive ```.config```. On y déclare toutes les pages avec la directive .state, en lui passant en paramètres: le nom qu’on souhaite donner (ici : main), suivi de l’url (ici : /main), de l’url du fichier contenant la page (ici : templates/main.html) et enfin le controller associé s’il y en a un (ici : ```MainCtrl```).

**ATTENTION : dans le cas d’une déclaration multiple, il ne faut surtout pas mettre de “;” après chaque noeud .state ! Le “;” doit être positionné sur le dernier noeud**

Enfin, la directive ```$urlRouteProvide.otherwise``` indique qu’elle est la première page à afficher

###Déclaration des controllers

(http://mcgivery.com/controllers-ionicangular/)

Les controllers sont créés dans le répertoire lib de l’application. Il n’est pas obligatoire de créer un fichier controller pour chaque vue. Cependant, chaque nouveau fichier controller doit être ajouté dans le head du ```index.html``` ```<script src="js/controller.js"></script>```

après l’appel de ```<script src="js/app.js"></script>```

Un controller se présente sous la forme suivante :

```
angular.module('starter.controllers', [])

.controller('ToDoListCtrl', function ($scope, $ionicModal) {

  // array list which will contain the items added
  $scope.toDoListItems = [{
    task: 'First task',
    status: 'not done'
  }, {
    task: 'Second task',
    status: 'not done'
  }];

  //init the modal
  $ionicModal.fromTemplateUrl('templates/modal.html', {
      scope: $scope,
      animation: 'slide-in-up'
  }).then(function (modal) {
      $scope.modal = modal;
  });

  // function to open the modal
  $scope.openModal = function () {
      $scope.modal.show();
  };

  // function to close the modal
  $scope.closeModal = function () {
      $scope.modal.hide();
  };
});
```

La directive ```.controller(‘monController’...``` permet de déclarer le controller. Elle prend en paramètre, son nom, une fonction de paramétrage qui est le corps du controller (avec un certain nombre de paramètre dont le $scope courant et les autres dépendances Angular nécessaires).
On assigne ensuite au $scope tout ce que l’on souhaite ex :

```
.controller('MainCtrl', function($scope) {
$scope.toDoListItems = [{
    		task: 'First task',
    		status: 'not done'
  	}, {
    		task: 'Second task',
    		status: 'not done'
  	}];
	$scope.firstName = "Andrew";
	$scope.lastName = "McGivery";
//functions…
function subtract(c,d){
		return c - d;
	}
	
	$scope.subtract = subtract;
...
})
```

**ATTENTION : un controller doit rester le plus simple possible, généralement il n’inclut que les fonctions utiles à la couche business pour une seule vue. On évite donc de déclarer plusieurs controllers liés à plusieurs vues dans le même fichier**

######Lier un controller avec des données provenant d’un service

ex de vue simple :

```
<ion-view title="About">
  <ion-content>
	My super cool content here! My name is {{user.name}}.
  </ion-content>
</ion-view>
```

directive factory retournant le nom d’utilisateur

```
.factory('userService', function($http) {
	return {
		GetUser: function() {
			  return {name: "Andrew"}
		},
	}
})
```

Binder les données provenant du service, vers la vue pour afficher le nom d’utilisateur:

```
.controller('MainCtrl', function($scope,userService) {
	$scope.user = userService.GetUser(); //Returns {name: "Andrew"}
})
```


Ensuite pour pouvoir utiliser un controller, il suffit d’utiliser la directive ng-controller au moment où l’on souhaite lui faire appel.

###Cibler une plateforme

(http://ionicframework.com/docs/platform-customization/platform-classes.html)
(http://ionicframework.com/docs/platform-customization/styling-angularjs.html)

```
ionic.Platform.isIOS()
```

```
ionic.Platform.isAndroid()
```

```
ionic.Platform.isWindowsPhone()
```

###Controllers

(http://ionicframework.com/docs/api/service/$ionicActionSheet/)

###Customisation des thèmes et couleurs

Par défaut les applications ionic utilisent le CSS. Il est toutefois possible de les personnaliser en utilisant Sass

**Initialiser Sass dans un projet**

```$ ionic setup sass (une fois le projet créé)```

(http://ionicframework.com/docs/cli/sass.html)

**Créer ses propres constantes (e.g config.json de Titanium)**

(http://ionicframework.com/docs/v2/theming/theming-your-app/)

**Définition de CSS properties avec Sass**

http://ionicframework.com/docs/v2/theming/sass-variables/

**Theme de l’application selon la plateforme**

(http://ionicframework.com/docs/v2/theming/platform-specific-styles/)

###Fonctions anonyme déconseillées

```
/* recommended */
function SessionsController() {
    var vm = this;
    vm.gotoSession = gotoSession;
    vm.refresh = refresh;
    vm.search = search;
    vm.sessions = [];
    vm.title = 'Sessions';
    ////////////
    function gotoSession() {
      /* */
    }
    function refresh() {
      /* */
    }
    function search() {
      /* */
    }
}
```

###Utilisation de l’appareil photo

Installer le package cordova.camera

(https://devdactic.com/how-to-capture-and-store-images-with-ionic/)

(https://www.thepolyglotdeveloper.com/2014/09/use-android-ios-camera-ionic-framework/)

###Utilisation de la géolocalisation

(http://blog.lahaxe.fr/2015/03/10/Ionic-geolocalisation/)

(http://ngcordova.com/docs/plugins/geolocation/)

##Vers ionic 2

(http://ionicframework.com/docs/v2/getting-started/migration/)
