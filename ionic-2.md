#ionic 2

> **Warning** this guide is based on the beta of ionic 2. Consequently, some information may be outdated

##### Table of Contents  
[Start with ionic](#start-with-ionic)  
[Grunt](#grunt)    
[Atom configuration](#work-with-atom)  
[Bracket](#bracket)     
[Cordova](#cordova)  
[Gulp](#gulp)  
[Useful functions](#useful-functions)  
[TypeScript](#typescript)  
[Angular 2](#angular-2)  
[Decorators](#decorators)    
[Pipe](#pipe)    
[Config](#config)    
[Global variables](#global-variables)     
[Third party lib](#third-party-lib)    
[Geolocation](#geolocation)  
[Database](#database)  
[Camera](#camera)   
[Barcode Scanner](#barcode-scanner)  
[HTTP query](#http-query)  
[Navigation](#navigation)  
[Themes](#themes)  
[Components (combobox, ion-list...)](#components)  
[File access](#file-access)  
[Backend Firebase](#backend-firebase)      
[Backend Strongloop](#backend-strongloop)     
[Internationalization](#internationalization)  
[Splash screen and appicon](#splash-screen-and-appicon)  
[Testing with Jasmine](#testing-with-jasmine)    
[Beta testing](#beta-testing)    
[Publishing App](#publishing-app)  
[Push notification](#push-notification)    

##Start with ionic

**Some resources**

[Link : ng-conf-workshop](https://github.com/chrisgriffith/ng-conf-workshop)    

[link : ionic.io](http://docs.ionic.io/docs/io-introduction)

[link : Official ionic 2 documentation](http://ionicframework.com/docs/v2/getting-started/migration/)

[link : Official ionic 2 native component documentation](http://ionicframework.com/docs/v2/native/Calendar/)

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
$ sudo npm install -g ionic@beta
```

**Updating ionic 2 framework**

```
$ npm install -g ionic@beta
```

again, and then updating the package.json file of your project. You should see something like 

this in that file:
```
 "dependencies": {
 "angular2": "2.0.0-beta.6",
 "es6-promise": "3.0.2",
 "es6-shim": "0.33.13",
 "ionic-angular": "2.0.0-beta.3",
 "ionic-native": "^1.0.12",
 "ionicons": "3.0.0-alpha.3",
 "reflect-metadata": "0.1.2",
 "rxjs": "5.0.0-beta.0",
 "zone.js": "0.5.14"
 }
```
Simply change the ionic-angular version number to the latest version, and then run:

```
npm install
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

##Grunt
[Back to top](#ionic-2) 

###1 Grunt (global) Install
```
$ npm install -g grunt-cli
```

###2 Next, installing Grunt into local project
```
$ npm install grunt --save-dev
```

###3 Create grunt file
```
$ touch Gruntfile.js
```
**Here's the basic structure of a grunt file :**
```
module.exports = function(grunt) {

  // Configuration de Grunt
  grunt.initConfig({})

  // Définition des tâches Grunt
  grunt.registerTask('default', '')

}
```

###4 Add Grunt task : convert scss file to css

```
$ npm install grunt-contrib-sass --save-dev
```

**Grunt file content**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {                              // Task's name
      dist: {                            // Sub-task's name
        options: {                       // Options
          style: 'expanded'
        },
        files: {                         // files's list
          'main.css': 'main.scss',       // 'target': 'source'
          'widgets.css': 'widgets.scss'
        }
      }
    }
  })

  // import
  grunt.loadNpmTasks('grunt-contrib-sass')

  // updating 'default' task which is running by defaul when grunt is running.
  // Here, we're define sass as a default task
  grunt.registerTask('default', ['sass:dist'])
}
```

**You can also give a folder instead of listing all the file one by one** 
```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{ // C'est ici que l'on définit le dossier que l'on souhaite importer
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass')

  grunt.registerTask('default', ['sass:dist'])
}
```

###5 Add Grunt task : concataining all JS files

```
npm install grunt-contrib-concat --save-dev
```

**Adding package to grunt file**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass');
  grunt.loadNpmTasks('grunt-contrib-concat'); // New package

  grunt.registerTask('default', ['sass:dist'])
}
```

**Add new task**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    },
    concat: {
      options: {
        separator: ';', // To insert ";" between each concatened file
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js'], // Source
        dest: 'dist/built.js' // Target
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass');
  grunt.loadNpmTasks('grunt-contrib-concat');

  grunt.registerTask('default', ['sass:dist', 'concat:dist'])	// Add the new task in default task
}
```

###6 Add Grunt task : Compressing all JS files

```
$ npm install grunt-contrib-uglify --save-dev
```

**Grunt file content**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    },
    concat: {
      options: {
        separator: ';'
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js'],
        dest: 'dist/built.js'
      }
    },
    uglify: {
      options: {
        separator: ';'
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js'],
        dest: 'dist/built.js'
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass')
  grunt.loadNpmTasks('grunt-contrib-concat')

  grunt.registerTask('dev', ['sass:dist', 'concat:dist']) // C'est pas chouette ça ?
  grunt.registerTask('dist', ['sass:dist', 'uglify:dist']) // Et hop, je compresse si je lance $ grunt dist
}
```

###7 Add automatic watcher

To avoid compilation after each file modification in your project, you can use a "watch" task.
```
$ npm install grunt-contrib-watch --save-dev
```

**Grunt file content**

```
module.exports = function(grunt) {

  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      }
    },
    concat: {
      options: {
        separator: ';'
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js'],
        dest: 'dist/built.js'
      }
    },
    uglify: {
      options: {
        separator: ';'
      },
      dist: {
        src: ['src/intro.js', 'src/project.js', 'src/outro.js']
        dest: 'dist/built.js'
      }
    },
    watch: {
      scripts: {
        files: '**/*.js', // All JS files
        tasks: ['concat:dist']
      },
      styles: {
        files: '**/*.scss', // All Sass files
        tasks: ['sass:dist']
      }
    }
  })

  grunt.loadNpmTasks('grunt-contrib-sass')
  grunt.loadNpmTasks('grunt-contrib-concat')
  grunt.loadNpmTasks('grunt-contrib-watch')

  grunt.registerTask('default', ['dev', 'watch'])
  grunt.registerTask('dev', ['sass:dist', 'concat:dist'])
  grunt.registerTask('dist', ['sass:dist', 'uglify:dist'])
}
```

###8 Cleaning Grunt file

```
module.exports = function(grunt) {

  // Je préfère définir mes imports tout en haut
  grunt.loadNpmTasks('grunt-contrib-sass')
  grunt.loadNpmTasks('grunt-contrib-concat')
  grunt.loadNpmTasks('grunt-contrib-watch')

  var jsSrc = ['src/intro.js', 'src/project.js', 'src/outro.js']
  var jsDist = 'dist/built.js'

  // Configuration de Grunt
  grunt.initConfig({
    sass: {
      dist: {
        options: {
          style: 'expanded'
        },
        files: [{
          "expand": true,
          "cwd": "src/styles/",
          "src": ["*.scss"],
          "dest": "dist/styles/",
          "ext": ".css"
        }]
      },
      dev: {} // À vous de le faire ! vous verrez que certaines options Sass sont plus intéressantes en mode dev que d'autres.
    },
    concat: {
      options: {
        separator: ';'
      },
      compile: { // On renomme vu qu'on n'a pas de mode dev/dist. Dist étant une autre tâche : uglify
        src: jsSrc, // Vu qu'on doit l'utiliser deux fois, autant en faire une variable.
        dest: jsDist // Il existe des hacks plus intéressants mais ce n'est pas le sujet du post.
      }
    },
    uglify: {
      options: {
        separator: ';'
      },
      compile: {
        src: jsSrc,
        dest: jsDist
      }
    },
    watch: {
      scripts: {
        files: '**/*.js',
        tasks: ['scripts:dev']
      },
      styles: {
        files: '**/*.scss',
        tasks: ['styles:dev']
      }
    }
  })

  grunt.registerTask('default', ['dev', 'watch'])
  grunt.registerTask('dev', ['styles:dev', 'scripts:dev'])
  grunt.registerTask('dist', ['styles:dist', 'scripts:dist'])

  // Give generics names
  grunt.registerTask('scripts:dev', ['concat:compile'])
  grunt.registerTask('scripts:dist', ['uglify:compile'])

  grunt.registerTask('styles:dev', ['sass:dev'])
  grunt.registerTask('styles:dist', ['sass:dist'])
}
```



##Work with Atom
[Back to top](#ionic-2) 

###1 - Install Atom

[link : Atom website](https://atom.io/)

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

[link : TODO-show configuration](https://atom.io/packages/todo-show)
```
$ apm install todo-show
```

[link : Minimap configuration](https://atom.io/packages/minimap)
```
$ apm install minimap
```

[link : Linter JSHint](https://atom.io/packages/linter-jshint)
```
$ apm install linter-jshint
```

[link : Linter CSS](https://atom.io/packages/linter-csslint)
```
$ apm install linter-csslint
```

[link : JSDoc](https://atom.io/packages/jsdoc)
```
$ apm install jsdoc
```

[link : Docblockr](https://atom.io/packages/docblockr)
```
$ apm install docblockr
```

####Activate auto-compilation

[tsconfig.json configuration](https://github.com/TypeStrong/atom-typescript/blob/master/docs/tsconfig.md)    
[Atom typescript plugin documentation](https://github.com/TypeStrong/atom-typescript)    

Create a **tsconfig.json** file in your project root with :

```
{
	"compileOnSave": false
}
```

####Shortcuts

```F6``` For compilation


##Bracket
[Back to top](#ionic-2) 

[link : Bracket official website](http://brackets.io/)
[link : Package ionic](http://www.ionicbrackets.com/)

After installation, download the ionicBracket plugin, then just open the extension manager inside of Brackets and copy the extension link (http://ionicbrackets.com/Ionic-Brackets-Extension.zip) into the extension url field and hit install.


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


##TypeScript
[Back to top](#ionic-2)  

[link : TypeScript Guildeline](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines)    

##Angular 2
[Back to top](#ionic-2)  

[link : become a ninja with Angular 2](https://books.ninja-squad.com/public/samples/Become_a_ninja_with_Angular2_sample.html)
[link : new Angular 2 concepts and syntax](http://www.joshmorony.com/ionic-2-first-look-series-new-angular-2-concepts-syntax/)
[link : Angular 2 syntax demistified](http://blog.thoughtram.io/angular/2015/08/11/angular-2-template-syntax-demystified-part-1.html)
[link : AngularUI](https://angular-ui.github.io/)

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
 
<li *ngFor="let item of items">
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

If you’ve used ngCordova then you will probably already be familiar with promises (a lot of JavaScript libraries implement promises) and why they are easier to use than callbacks. Promises provide a much nicer format for grabbing asynchronous data (e.g. data you need to wait for when you fetch something from a server or device), the current format of callbacks leads to ugly nested code that can become a nightmare to maintain.

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

[link : Decorators by Josh MORONY](https://www.joshmorony.com/building-mobile-apps-with-ionic-2/decorators-in-ionic2.html)

####@App
**@App** is the most important decorator of all, but you'll only ever use it once in each application you build. **The @App decorator declares the class that it is attached to as the root component of the application**. We've already talked about this briefly, and will continue to do so later, but the root component is essentially the starting point for your app.

It's important to understand the component based structure of an Ionic 2 application, it's basically made up of a bunch of different components tied together, and at the root of all of **this is the root component**. The root components main responsibility is setting up your root page, which will be the first page that the user sees in your application. You can then get your page to push additional pages onto the navigation stack (we will cover navigation concepts in depth in a later lesson), and those pages can in turn push more pages and so on.

####@Page
**@Page** is likely the most common decorator you will use in your applications. It is used to define any page, or "view", in your application. So if you have an application with the following pages:

- Location
- All Products
- Product Detail
- Contact

Then **each of these will be their own components which will have a decorator of @Page in the class definition**. Every page will also have a template that can either be defined directly using template in the decorator, or by using a templateUrl

```
@Page({
    templateUrl: 'build/pages/location/location.html'   
})
export class LocationPage {

}
```

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

[link : Understanding Pipe](http://mcgivery.com/understanding-ionic-2-pipe/)

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

##Pipe
[Back to top](#ionic-2)  

[link : Understanding Pipe](http://mcgivery.com/understanding-ionic-2-pipe/)      
[link : Josh Morony Pipe documentation](http://www.joshmorony.com/how-to-use-pipes-to-manipulate-data-in-ionic-2/)

####First step : create the pipe class

First, create a "pipe" directory in your project will containing all pipe lib. A basic pipe class looks like below :

```
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

```
export class HelloWorldPipe implements PipeTransform {
	// Pipe function
	transform(value) {
		return "Hello " + value + "!";
	}
}
```

####Using pipe in other page

```
import {HelloWorld} from 'pipes/HelloWorld';	// pipe import

@Page({
	templateUrl: 'myPage/myPage.html',
	pipes: [HelloWorld]	// pipe declaration
})
export class MyPage {
	constructor(){
		this.name = "Andrew";
	}
}
```

**View file**

Pipe inline syntax : ```value | myPipe:args[0]:args[1]```

```
<ion-label>{{name | helloWorld}}</ion-label>
```

**Note:** The first letter of the pipe's name in the view file is in lower case

####Other example

**Pipe file**

```
import {Pipe} from '@angular/core';

@Pipe({
	name: 'addInt'
})
export class AddInt {
	transform(value, args) {
		return value + args[0];
	}
}
```

**Page file**

```
import {AddInt} from 'pipes/AddInt';

@Page({
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

**View file**

```
The meaning of life: {{mySingleInt | addInt:2}}

<ul>
<li *ngFor="let myInt of myIntArray">
{{myInt | addInt:1}}
</li>
</ul>
```

####Conclusion

Pipes are very useful for string formatting like date, hour, regexp...

##Config
[Back to top](#ionic-2)  

The Config lets you configure your entire app or specific platforms. You can set the tab placement, icon mode, animations, and more here.

[link : Config official documentation](http://ionicframework.com/docs/v2/api/config/Config/)

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

##Global variables
[Back to top](#ionic-2)

Here's a solution to centralize application's globals. The solution consist in using **config.js** file in provider's folder.

You can export all your variable like below :

```
export let VALUE_ONE = "09:00";
export let VALUE_TWO = "192.168.0.1";
...
```

And then in the component or service that requires them, just do this :

```
import {VALUE_ONE} from './config';
```

##Third party lib
[Back to top](#ionic-2)

To use a custom lib file in your project, follow the next steps 

**1 Create "lib" folder under app**

```
/app/lib/utils.js
```

**2 implement lib file**

ex : utils.js
```
var UI = {};

UI.info = function(_titre, _message){
  _titre = _titre != "" ? _titre : "";
  _message = _message != "" ? _message : "";
  
  console.log(`[--- ${_titre} ---] ${_message}`);
};

export UI;

```
or export only some functions

```
export function getSquare(_value){	// Only this function will be available from external
   return square(_value);
}

function square(_value){	// Not exported
   return _value * _value;
}
```

**3 Using the custom lib in the whole project**

ex : From Home.js page
```
import * as UI from '../../lib/utils';

@Page({
  templateUrl: 'build/pages/home/home.html'
})
export class HomePage {

  //Chargement de la base de données
  constructor() {
    UI.info("test","toto"); 
  }
}
```

**4 TODO : to test
```
//  lib/math.js
LibMath = {};
LibMath.sum = function (x, y) { return x + y };
LibMath.pi = 3.141593;
```

```
//  someApp.js
var math = LibMath;
console.log("2π = " + math.sum(math.pi, math.pi));
```

```
//  otherApp.js
var sum = LibMath.sum, pi = LibMath.pi;
console.log("2π = " + sum(pi, pi));
```

##Geolocation
[Back to top](#ionic-2)  

[link : google map geolocation](http://www.joshmorony.com/ionic-2-how-to-use-google-maps-geolocation-video-tutorial/)

**Adding Google Map API depency in index.html**

```
<script src="http://maps.google.com/maps/api/js"></script>
<script src="cordova.js"></script>
<script src="build/js/app.bundle.js"></script>
```

**Important** During production deployment, you will have to create Google MAP API key and put it in parameter

**cordova plugin installation**

```
$ ionic plugin add cordova-plugin-geolocation
```

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

##Database
[Back to top](#ionic-2)  

[link : Using Sqlite storage tutorial](https://devdactic.com/ionic-2-sqlstorage/)

###First solution
There is two main solutions for data storage. The first one is the local HTML5 storage and the second is using SQLite database storage.

[link : using sqlite](https://www.thepolyglotdeveloper.com/2015/12/use-sqlite-in-ionic-2-instead-of-local-storage/)

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
        <ion-item *ngFor="let person of people">
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

####Resources

[Google chrome PouchDB inspector extension](https://chrome.google.com/webstore/detail/pouchdb-inspector/hbhhpaojmpfimakffndmpmpndcmonkfa?hl=en)    

[Ionic 2 - PouchDB tutorial](http://gonehybrid.com/how-to-use-pouchdb-sqlite-for-local-storage-in-ionic-2/)    

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

View file

```
<ion-navbar *navbar maintheme>
  <button menuToggle>
    <ion-icon name="menu"></ion-icon>
  </button>
  <ion-title>Photo</ion-title>
</ion-navbar>

<ion-content padding class="getting-started">
    <img src="{{sourceImage}}"/>
	<button fab primary fab-bottom fab-center (click)="takePhoto()">
         <ion-icon name="camera"></ion-icon>
    </button>
</ion-content>

```

Controller file
```
import {Page} from 'ionic-angular';
import {Camera} from 'ionic-native';

@Page({
  templateUrl: 'build/pages/photo/photo.html'
})
export class PhotoPage {
    constructor(){
        this.sourceImage = "";
    }

    takePhoto(){
        let options = {
          quality: 100,
          destinationType: navigator.camera.DestinationType.FILE_URI,
          sourceType: navigator.camera.PictureSourceType.CAMERA,
          encodingType: navigator.camera.EncodingType.JPEG,
          saveToPhotoAlbum: true
        };

        navigator.camera.getPicture(
          (imagePath) => {
            console.log(imagePath);
            this.sourceImage = imagePath;
          },

          (error) => {
            console.log(error);
          }, options
        );
    }
}

```

[link : List of camera options](https://github.com/apache/cordova-plugin-camera#module_camera.CameraOptions)


##Barcode scanner
[Back to top](#ionic-2)

[link : Barcode scanner documentation](http://ionicframework.com/docs/v2/native/BarcodeScanner/)

##HTTP query
[Back to top](#ionic-2)  

[link : using http](http://www.joshmorony.com/using-http-to-fetch-remote-data-from-a-server-in-ionic-2/)

[link : reddit API url for testing app](https://www.reddit.com/r/gifs/top/.json?limit=10&sort=hot)

**Create the view (page.html)**

```
<ion-navbar *navbar>
  <ion-title>Tab 1</ion-title>
</ion-navbar>
 
<ion-content>
  <ion-list>
    <ion-item *ngFor="let post of posts">
      <img [src]="post.data.thumbnail" />
    </ion-item>
  </ion-list>
</ion-content>
```

**Create controller (page.js)**

```
import {Page} from 'ionic/ionic';
import {Http} from '@angular/http';
import 'rxjs/add/operator/map';
 
@Page({
  templateUrl: 'build/pages/page/page.html'
})
export class Page {
  static get parameters() {
     return [[Http]];
  }

  constructor(http) {
 
    this.http = http;
    this.posts = null;
 
    this.http.get('https://www.reddit.com/r/gifs/new/.json?limit=10').map(res => res.json()).subscribe(data => {
        this.posts = data.data.children;
    });
 
  }
}
```

#####Note : 
The **map** lib is only imported because we need is http.get function

##Navigation
[Back to top](#ionic-2)  

###Using NavController

[link : Understanding ionic 2 NavController](http://mcgivery.com/understanding-ionic-2-navigation-navcontroller/)

Before we can use the NavController, we will need to import it.

```
import {Page, NavController} from 'ionic-angular';
```

Next we will inject it into our ```@Page``` and assign it to a property.

```
import {Page, NavController} from 'ionic-angular';

@Page({
	templateUrl: "build/pages/Main/Main.html"
})
export class MainPage(){
	constructor(nav: NavController){
		this.nav = nav;
	}
}
```

Now, we can call properties on nav, our instance of **NavController**. For example, say we want to navigate from our Main view to our About view, we would need to start by importing that ```@Page``` class.

```
import {Page, NavController} from 'ionic-angular';
import {AboutPage} from 'About/About'

@Page({
	templateUrl: "build/pages/Main/Main.html"
})
export class MainPage(){
	constructor(nav: NavController){
		this.nav = nav;
	}
}
```

Next, let’s create a method on our page called **goToAbout** that we can call from our template. This method will push the AboutPage onto the stack.

```
import {Page, NavController} from 'ionic-angular';
import {AboutPage} from 'About/About'

@Page({
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

```
<button (click)="goToAbout()">About</button>
```

To summarize, when this button is pressed, it will call the goToAbout method which pushes an instance of the AboutPage class onto the navigation stack which is then compiled and animated into view.

####Passing Data
In many scenarios we have data in one view that we need to pass to another. Luckily, the push method accepts a second parameter which is an object of data to pass to the ```@Page``` passed into the first parameter.

```
this.nav.push(AboutPage,{
	username: "andrewmcgivery",
	blogger: true
});
```

This data is then accessible in the pushed ```@Page``` via navParams which is similar to $stateParams in 1.0.

```
import {Page, NavParams} from 'ionic-angular';

@Page({
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

```
import {Page, NavController} from 'ionic-angular';

@Page({
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
In version 1.0, we had the concept of events being fired when we were entering and leaving the view, among others. In version 2.0, we have a very similar set of events. To handle one of these events, we just need to give our ```@Page``` class a method that matches the event. For example, if we want to run an event when the ```@Page``` is loaded, we will need to give our page the **onPageLoaded** method:
```
import {Page} from 'ionic-angular';

@Page({
	templateUrl: 'build/pages/About/About.html',
})
export class AboutPage {
	onPageLoaded(){
		console.log("Page Loaded!");
	}
}
```

We can have a set of handlers for a variety of events including then the page is about to be entered, when the page is leaving, etc. Again, I would suggest reading the Official Docs.

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
<ion-item>
	<ion-label>Profession</ion-label>
	<ion-select [(ng-model)]="prof">
		<ion-option *ngFor="let item of professions" value="{{item.objectId}}">{{item.titre}}</ion-option>
	</ion-select>
</ion-item>
```

###ion-list

Solution for filling dynamic ion-list item

```
<ion-list> 
    <ion-item *ngFor="let item of items">{{item.fullname}}</ion-item> 
</ion-list>

or
```

For clickable list you have to use 

```
<ion-list> 
    <button ion-item *ngFor="let item of items">{{item.fullname}}</button> 
</ion-list>
```


**Add filter on ion-list**

Consider a ion-list in which we want to hide every items which property "deleted" is set to true

```
<ion-list>
  <ion-item-sliding *ngFor="let item of getActiveItems()" #slidingItem>
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
    <ion-item-sliding *ngFor="let post of posts">
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

####ion-item-sliding

```
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
        <button darkgrey (click)="removeNote(item)" class="btn"><ion-icon name="trash"></ion-icon>Delete</button>
      </ion-item-options>
    </ion-item-sliding>

  </ion-list>
</ion-content>
```

####Inifinite scroll in ion-list

#####Solution 1

[link : Scroll performance](http://www.joshmorony.com/boosting-scroll-performance-in-ionic-2/)
[link : virtual-scroll official doc](http://ionicframework.com/docs/v2/api/components/virtual-scroll/VirtualScroll/)

**Create new project**

```
ionic start virtual-scroll tabs --v2
```

**Create Data**

Modify Page1 and Page2 controller with :

```
import {Page} from 'ionic-angular';


@Page({
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
```
<ion-navbar *navbar>
  <ion-title>
    Standard Scroll
  </ion-title>
</ion-navbar>
 
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

```
<ion-navbar *navbar>
  <ion-title>
    Virtual Scroll
  </ion-title>
</ion-navbar>
 
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

View file
```
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

###Searchbar

```
<ion-searchbar [(ngModel)]="searchQuery" (change)="searchThing($event)" autocorrect="off"></ion-searchbar>
```

```
searchThing() {
this.giphy.search(this.searchQuery).then(data => {
    this.gifs = data;
});
```

###Alert dialog box

Here's a sample code to show a confirmation dialog box. The key is to add Alert import and then, don't miss to add alert object to current navigation stack

```
import {Page, NavController, Alert} from 'ionic-angular';
import {Data} from '../../providers/data/data';

@Page({
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

##File access
[Back to top](#ionic-2)  

[link : save image locally](https://forum.ionicframework.com/t/how-to-save-an-image-locally-with-ionic-2/46257/4)

##Backend Firebase
[Back to top](#ionic-2)  

##Backend Strongloop
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

##Splash screen and appicon
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

**Remove spinner**
Add the following property to config.xml
```
<preference name="ShowSplashScreenSpinner" value="false"/>
```

##Testing with Jasmine
[Back to top](#ionic-2)

##Beta testing
[Back to top](#ionic-2)

Available for iOS and Android, Ionic View makes it easy to **test** and **share** your app directly **on the device**. **A developer, client, customer, or friend** can download Ionic View, enter the App Id for your app, and immediately load and test the app. With hundreds of thousands of installs, Ionic View is becoming a core part of the Ionic development experience.

[link : Ionic View](http://blog.ionic.io/rapid-development-with-ionic-view/)

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


##Push notification
[Back to top](#ionic-2) 

First way, using push notification module, only works when app is opened

```
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
      console.log('ONLY WORK'S WHEN APP IS OPEN')
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

```
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

```
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
