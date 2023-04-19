[< Back to main Menu](https://github.com/gsoulie/Mobile-App-Development)    

# Mobile App Resources and tools

## Form factor screen breakpoints

👉 0px - 480px - small phones

👉 481px - 768px - Tablets / big phones. 

👉 769px - 1279px - Laptop

👉 1280px+ - Computer and Wide screens

````@media screen and (max-width: 480px){}````

## Markdown diagrams

````mermaid
stateDiagram-v2
  [*] --> Still
  Still --> [*]
  
  Still --> Moving
  Moving --> Still
  Moving --> Crash
  Crash --> [*]
````

````mermaid
stateDiagram-v2
  [*] --> Frontends
  [*] --> Backends
  
  Frontends --> Angular
  Frontends --> Ionic
  Ionic --> Angular
  Frontends --> React
  Frontends --> Vue3
  Backends --> NodeJS
  Angular --> JS
  Ionic --> JS
  React --> JS
  Vue3 --> JS
  NodeJS --> JS
  JS --> [*]
````

````mermaid
stateDiagram-v2
[*] --> Rendering

Rendering --> Where?
Where? --> Browser
Browser --> Client-Side Rendering (CSR)
Where? --> Server
Server --> When?
When? --> At build time
At build time --> Prerendering / Static Site Generation (SSG)
When? --> With a client request
With a client request --> Server-Side Rendering (SSR)
````

## Framework frontend

https://materializecss.com/      

## PWA

[Features available](https://whatwebcando.today/)    

## Accessibility

- https://randoma11y.com/      

## Tools

[https://institutnr.org/outils-ecoconception-accessibilite](https://institutnr.org/outils-ecoconception-accessibilite)       

## Graphical resources

### Icônes font et svg gratuites
- [https://icones.js.org/](https://icones.js.org/)      

### Gradiant generators

- [Personnal collection](https://github.com/gsoulie/ionic-angular-snippets/blob/master/gradiant.md)      
- [Josh Comeau Gradient generator](https://www.joshwcomeau.com/gradient-generator/)     
- [Gradient color palette](https://dribbble.com/shots/13662178-Gradients/attachments/5267324?mode=media)      
- [https://cssgradient.io/](https://cssgradient.io/)    
- [https://mycolor.space/gradient](https://mycolor.space/gradient)     
- [https://www.colorzilla.com/gradient-editor/](https://www.colorzilla.com/gradient-editor/)     
- [https://www.cssmatic.com/gradient-generator](https://www.cssmatic.com/gradient-generator#'\-moz\-linear\-gradient\%28left\%2C\%20rgba\%28248\%2C80\%2C50\%2C1\%29\%200\%25\%2C\%20rgba\%28241\%2C111\%2C92\%2C1\%29\%2050\%25\%2C\%20rgba\%28246\%2C41\%2C12\%2C1\%29\%2051\%25\%2C\%20rgba\%28240\%2C47\%2C23\%2C1\%29\%2071\%25\%2C\%20rgba\%28231\%2C56\%2C39\%2C1\%29\%20100\%25\%29\%3B')

### Drop shadow generators
- https://getcssscan.com/css-box-shadow-examples       
- https://dropshadow.io/      
- http://css3studio.com/page-css3/css-box-shadow.php      

[Loading.io](https://loading.io/)    
[Ionic color generator](https://ionicframework.com/docs/theming/color-generator)    
[Imageoptim](https://imageoptim.com/fr.html)    
[Paletton](http://paletton.com/#uid=23q0u0k++VBrKZTEz+V+VxYZ+pL)    
[FlatUI colors](http://flatuicolors.com/)     
[Material Design palette](http://www.materialpalette.com/)         
[Color trends by OS](http://tintui.com/index.html)     
[Material design](http://www.google.com/design/spec/style/color.html#color-color-palette)    
[Android official icons](https://developer.android.com/design/downloads/index.html)   
[Adobe color CC](https://color.adobe.com/fr/explore/newest/)    
[Icon pack for prototyping](https://fr.icons8.com/web-app/category/ios7/Photo-Video)    
[Icon pack for prototyping 2](https://thenounproject.com/)    
[Favicon Generator](https://www.favicon-generator.org/)    

## Tools

[sequence diagram tool](https://www.websequencediagrams.com/)    

## Editor

[Visual Studio Code](http://code.visualstudio.com/Docs/?dv=osx)    

## material.angular.io

[material.angular.io](https://material.angular.io/)     

## Git
[Simple Git guide](http://rogerdudler.github.io/git-guide/index.fr.html)  

## Printable A4 sketch template
[Printable A4 sketch](https://androiduiux.com/2013/01/06/printable-a4-screen-flow-sketch-template-free-download/)    

## Device screen size

[Devices metrics](http://www.materialup.com/posts/device-metrics-google-design)    
[Devices width](https://mydevice.io/devices/#sortTablets)    

## JS / TypeScript Guideline

[bevacqua](https://github.com/bevacqua/js/blob/master/README.md)    
[TypeScript Guildelines](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines)    

## JS Libraries

[IS.JS](http://arasatasaygin.github.io/is.js/)    
[Dayjs](https://day.js.org/docs/en/installation/installation)    

## JS tools
  
[JSONLint](http://jsonlint.com/)    
[JSHint](http://jshint.com/)    
[JSON editor](http://www.jsoneditoronline.org/)    
[JSON viewer](http://jsonviewer.stack.hu/)     
[JSON Schema](http://jsonschema.net/#/)    
[TSLint for linting TypeScript code](http://palantir.github.io/tslint/)    

## Fonts
[font google](https://fonts.google.com/specimen/Nunito?selection.family=Nunito)    
[Icomoon](https://icomoon.io/)     
[FontSquirrel](http://www.fontsquirrel.com/)     

## App distributing
[InstallR](https://www.installrapp.com/)     

## Apple resources
[iOS Console](http://lemonjar.com/iosconsole/)    
[Average App Store Review Times](http://appreviewtimes.com/)     
[iOS icons generator for apple store](http://appicontemplate.com/ios8)     
[iPhone mockup](http://appicontemplate.com/iphonescreenshot)      
[iPad mockup](http://appicontemplate.com/ipadscreenshot)     
[printable sketch](http://sketchsheets.com/)     
[Install Certificates on new Mac](https://www.digicert.com/ssl-support/p12-import-export-mac-mavericks-server.htm)    

## Android resources
[Tools for icon, launch icon...](https://romannurik.github.io/AndroidAssetStudio/index.html)    
[Device Metrics](https://material.io/devices/)    
[Google Play Developer Console](https://play.google.com/apps/publish)    
[ActionBar generator](http://jgilfelt.github.io/android-actionbarstylegenerator/)     
[Android icon generator for Google Play Store](http://appicontemplate.com/android)     
[Material color generator](http://paletton.com)     

## Deeplinking
[beanch.io](https://branch.io/)    

## File transfer
[jaguar](http://share.jaguar-network.com/)      
