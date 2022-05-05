# Ionic Framework resources

> **Work in progress** : updating repos with new ionic 5 and Capacitor 3.0 usage

## Ionic en quelques mots

Ionic est un framework javascript, basé sur Angular et Typescript. Il permet de créer des applications mobiles hybrides basées sur les technologies web (html, css, js). Il permet aussi
de déployer des application mobile native Andoird / iOS.

Lorsqu'il est exécuté sur mobile, Ionic s'exécute dans un conteneur natif à l'aide de Capacitor, 
ce qui permet un accès complet à toutes les fonctionnalités ou API de l'appareil natif.

l'UI de ionic est exécuté dans une WebView qui est un navigateur sans en-tête. En mode web, le code est directement exécuté dans le 
navigateur.

Les composants UI utilisés par ionic utilisent les standards Web Components, de fait ils peuvent être exécutés dans n'importe quel 
navigateur et sont compatibles avec tous les frameworks JS / React / Vue et Angular.


##### Table of Contents  

* Good Start
	* [Devdactic Ionic 5 App navigation with Login, Guards & Tabs Area](https://github.com/gsoulie/ionic-capacitor-starter)       
* [Prerequisites](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-prerequisites.md)    
	* Update environment npm / nodejs
	* Chrome inspect device
	* Using gulp
	* Android debugging with logcat
	* Using multiple version of Node with nvm
	* Switching to ESLint
* [Concepts](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-concepts.md)    
	* Angular 2
	* Decorators
	* Pipe    
	* RxJS operators     
	* Promise vs Observable (map and subscribe operators)    
	* Observable and operators      
	* BehaviorSubject    
	* Arrow function
	* Async / Await functions     
	* Resolver     
	* Environments DEV / PROD     
	* Function declaration       
* [Capacitor](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-capacitor.md)    
	* Capacitor 3.0       	
	* Requirements      
	* Build     
	* Appicon and Splash screen     
	* Storage and Database : Local Storage, Caching API response, SQLite       
	* Listening Internet connection      
	* Haptics      
	* Android permissions      
	* Photo (PWA and Mobile)   
	* Azure pipeline CI/CD     
	* Live reload     
	* Azure msal authentication with Capacitor Msal plugin     
* [Directives](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-directive.md)    
* [Config](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-config.md)    
	* App platform specific behaviour configuration
	* Mapping 	
	* Color generator (add custom color) https://ionicframework.com/docs/theming/colors#new-color-generator      
* [Useful functions](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-useful-functions.md)  
	* Find element in array
	* Ionic Angular snippets
	* Properly display error
	* Get platform info
	* Generate UUID
	* Show / hide DOM element
	* Accessing DOM element @ViewChild
	* Show - Hide DOM element by screen size
	* Switch statement with complex expression
* [Phone call and Social sharing](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-phone.md)    
	* Phone call
	* Social sharing
* [Local Storage](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-local-storage.md)    
* [Firebase Services (need to be updated for Capacitor 3.0)](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-firebase-angularfire2.md#angularfire2)    
	* CRUD angularfire2    
	* Demo example     
	* Authentication    
	* Firebase rules    
	* Add data with custom key    
	* angularfire issue    
	* Querying on Firebase    
	* Firebase Cloud functions     
	* Firebase hosting
	* Lazy loading on firebase dataset    
	* Multiple database    
	* Firestore    
* [PWA](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-pwa.md)    
	* Make a pwa with photo and geolocation      
* [Navigation](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-navigation.md)  
	* Navigation by routing    
	* Routing params    
	* Reset Routing params    
	* Child routes    
	* Tab Routing    
	* Passing static data to a Route     
	* Passing dynamic data to a Route     
	* Routing Guards    
	* Wildcard route (404)   
	* Passing Data
	* Passing Data on close event
	* Disable Android hardware back button    
	* Navigating in modal with ion-nav     
	* Routing static html file     
* [Styling](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-sass.md)
	* Component variables     
	* Using variables    
	* Add color   
	* Get color variables from variable.scss   
	* Set transparent color to element    
	* Configure NavBar color    
	* Set transparent NavBar    
	* Set background image to content    
	* Lock screen orientation    
	* Positioning    
	* Remove Android input green highlight    
	* Styling Searchbar     
	* Disable scrolling on ion-content     
	* Label with full width inside ion-item     
	* Change ion-item height     
	* Split screen in two views    
	* Modale with overlay    
	* Remove ion-card shadow    
	* Remove header shadow    
	* Dynamic class    
	* Spacer   
	* Increase ion-icon size    
	* Remove header border    
	* Create CSS stepper    
	* Transparent scroll    
	* Create fixed menu with scrollable content   
	* Flex grid    
	* Flex box    
	* Make modale flexible    
	* 2 columns layout      
	* &::before and &::after       
	* Popover      
	* Accessing shadow parts      
	* Text overflow ellipsis       
* [Themes](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-theme.md)  
	* Dynamic theming
	* Navbar
	* StatusBar
	* Change background color of a specific page
	* Override Sass variable
	* Remove Android input green highlight
	* Remove android navbar border
	* Custom fonts    
* [UI Components](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-ui-component.md)    
	* ion-button
	* ModalController
	* ion-select
	* ion-item
	* ion-list
	* pagination
	* ion-label
	* ion-searchbar
	* list filtering
	* ion-tab
	* tab icon
	* ion-fab
	* ion-grid
	* ion-toggle
	* dynamic style
	* Toggle menu
	* Expandable header
	* List accordion
	* Picker
	* round progress bar
	* Swiper (replace ion-slide from v6)     
	* ion-slide (deprecated since v6)     
	* Hiding header on scroll
	* Notification badge on icon
	* Input with autocomplete datalist
	* Action sheet customization
	* ion-toast
	* ion-sliding-item swipe to delete
	* swipe to delete with gesture
	* iOS keyboard scroll      
	* ion-range    
	* ion-title      
	* ion-datetime      
* [Gesture](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-gesture.md)      
	* Swipe on ion-list with animation
* [Chart](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-chart.md)
	* Chartjs     
	* Angular issues      
	* Chart grid 50%    
	* ng2-google-chart worldmap      
	* Chart customization     
* [File](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-file-storage.md)  
	* Capacitor FileSystem    
	* File size    
	* Write file in PWA    
	* Loading Json File    
	* File upload with file explorer    
	* Open file with native system viewer    
* [Geolocation](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-geolocation.md)  
	* Angular2 Google maps integration    
	* Customize map markers    
	* Reverse geocoding    
	* Geolocation on capacitor    
	* Using Google Map navigation      
	* Leaflet and Mapbox      
* [Google Map integration](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-google-map-agm.md)    
* [Camera](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-camera.md)   
* [Gallery](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-gallery.md)    
* [HTTP queries](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-http-query.md)  
	* api-helper service     
	* PUT query    
* [Events](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-events.md)    
	* Page event
	* Event propagation    
* [Screen Orientation](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-screen-orientation.md)        
* [Custom Component](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-custom-component.md)   
	* Alert component    
	* Working example    
	* Popover example capacitor    
* [Animation](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-animation.md)  
	* Rotating Border animation     
	* Resources     
* [Known issues](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-known-issues.md)    
	* Display carriage return \r\n    
	* Remove iOS cache    
	* Gradle build failure app:debugCompileClasspath
	* iOS 12 keyboard issue    
	* iOS 12 Webview issue    
	* Typescript error    
	* iOS xcassets error - Distill failed for unknown reasons    
	* Android build failed In <declare-styleable> FontFamilyFont    
	* CORS issues    
	* HTTP query issues
	* Android build error    
	* Android Failed to execute aapt    
	* ViewDestroyError      
	* Updating nodejs for window    
	* Cannot read property id of undefined    
	* npm ERR! code EINVALIDPACKAGENAME      
* [Using image](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-using-images.md)   
	* Background image    
	* SVG    
	* Using cascading SVG    
	* Add blur    
	* Upload image    
	* Converting base64 string to blob	 
	* Lazy loading      
* [Forms](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-forms.md)    
	* NgModel Forms    
	* Form in Ionic 4    
* [Backends](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-backend.md)    
	* [Communicating between Ionic app and NodeJS backend](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-nodejs-backend.md)    
	* Strongloop
	* Firebase
* [Authentication](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-authentication.md)  
	* SSO with IS4 and redirect with Capacitor      
	* Ionic appauth         
	* Ionic Auth    
* [Internationalization](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-i18n.md)  
* [Splash screen and appicon - Cordova](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-splashscreen.md)  
* [Beta testing](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-beta-testing.md)    
* [Push notification](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-push-notification.md)   
* [Build for Android](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-build-android.md)  
* [Build for iOS](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-build-ios.md)    
	* Adding iOS permissions to plist automatically    
	* Restrict plist to iphone only    
* [Publishing App](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-publishing.md)  
	* Android     
	* Publishing with cordova (old)     
	* iOS      
* [Other modules](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-other-modules.md)   
	* CRC computation
* [Self working components](https://github.com/gsoulie/Ionic2-snippets)    
* [Debug Ionic Application](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-debug.md)    
* [Cloud testing](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-unit-testing.md)    
* [Bluetooth](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-bluetooth.md)    
	* BLE
	* Bluetooth Serial
* [Code documentation](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-code-documentation.md)    
* [Drawing](https://devdactic.com/ionic-canvas-drawing-files/)    
* [PDF export](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-html2pdf.md)    
	* html2pdf      
	* css print      
[TODO](https://github.com/gsoulie/ionic2-resources/blob/master/ionic-todo.md)      
