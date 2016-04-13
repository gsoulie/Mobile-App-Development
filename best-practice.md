#Best practice guide

> **Under construction**

[SASS](#sass)     
[Javascript](#javascript)    
[Ionic 2](#ionic-2)    
[AngularJS 2](#angularjs-2)    
[TypeScript](#typescript)    
[Commit](#commit)    
[iOS provisioning profile](#ios-provisioning-profile)   
[Comments](#comments)    
[Publishing](#publishing)    

##Sass
[Back to top](#best-practice-guide) 

[link : Sass best practice documentation](https://sass-guidelin.es/fr/#syntaxe--formatage)

**Display block**

```
.foo {
  display: block;
  overflow: hidden;
  padding: 0 1em;
}
```

**Variable**

```
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

**Encoding**

It's recommanded to force encoding in the main sass file with ```@charset```directive

```
@charset 'utf-8';
```

**Quote**

Quotes are not necessary but it's recommanded to use single quote for string. 

```
// Yep
$direction: 'left';

// Nope
$direction: left;
```

> **Warning** some values are specific for CSS and they don't need quote :

```
// Yep
$font-type: sans-serif;

// Nope
$font-type: 'sans-serif';
```

Strings which are containing single quote :

```
// Okay
@warn 'You can\'t do that.';

// Okay
@warn "You can't do that.";
```

**Decimal values**

```
// Yep
.foo {
  padding: 2em;
  opacity: 0.5;
}

// Nope
.foo {
  padding: 2.0em;
  opacity: .5;
}
```

**List**

```
// Yep
$font-stack: ('Helvetica', 'Arial', sans-serif);

// Yep
$font-stack: (
  'Helvetica',
  'Arial',
  sans-serif,
);

// Nope
$font-stack: 'Helvetica' 'Arial' sans-serif;

// Nope
$font-stack: 'Helvetica', 'Arial', sans-serif;

// Nope
$font-stack: ('Helvetica', 'Arial', sans-serif,);
```

**Extend/Inheritance**

This is one of the most useful features of Sass. Using ```@extend``` lets you share a set of CSS properties from one selector to another

```
.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.success {
  @extend .message;
  border-color: green;
}

.error {
  @extend .message;
  border-color: red;
}

.warning {
  @extend .message;
  border-color: yellow;
}
```

##Javascript
[Back to top](#best-practice-guide) 

[link : Javascript guideline](https://github.com/bevacqua/js/blob/master/README.md)    

**Using single CamelCase**

It's recommanded to use single CamelCase syntax for the function, like :

```
far firstLaunch = true;

function loadData(){
  ...
};
```

An exception for CommonJS module, put the first letter upper :

```
var Network = require('Network');

Network.httpRequest({
  ...
});
```

**Avoid plural**

**Avoid accent**

**Avoid get / set prefixes**

**Using upper case for constants**

**Avoid "_" prefix**

**Functionnal domain separators**

```
/**
 * LIBS -------------------------------------------------------------
 */
var Cloud = require('ti.cloud'),
    Moment = require('alloy/moment');
 
/**
 * INIT -------------------------------------------------------------
 */
var args = arguments[0] || {};

/**
 * FUNCTION ---------------------------------------------------------
 */
```
Use uppercase and "-" (until column 70)

##Ionic 2
[Back to top](#best-practice-guide) 

**Page name**

Use upper case on the first letter

##AngularJS 2
[Back to top](#best-practice-guide) 

##Typescript
[Back to top](#best-practice-guide)  

[link :Typescript guideline](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines)     

####Names
1. Use PascalCase for type names.
2. Do not use "I" as a prefix for interface names.
3. Use PascalCase for enum values.
4. Use camelCase for function names.
5. Use camelCase for property names and local variables.
6. Don't use "_" as a prefix for private properties.
7. Use whole words in names when possible.


####null and undefined

Use **undefined**, do not use null.

####Quotes

Use double quote for strings

####Basic types

[link : Basic types guideline](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Basic%20Types.md)    

####Classes

[link : Classes guideline](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Classes.md)    

####Namespace

[link : Namespace guideline](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Namespaces%20and%20Modules.md)    
####Function

[link : Function guideline](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Functions.md)    



##Commit
[Back to top](#best-practice-guide)    

_[page] - [element] : [(#ticket number) / description]_

_UserLogin - loginFunction : #123451 success case message updating_

##iOS provisioning profile
[Back to top](#best-practice-guide)    

To get more clarity in the provisioning profile list on Apple developer account, it's recommanded to format profile's name like :

`[CUSTOMER NAME]_[PROJECT NAME]_[PROFILE ENV]_[USER INITIALS (optionnal)]`

or

`[PROCJECT NAME]_[PROFILE ENV]_[USER INITIALS (optionnal)]`

or

`[APPID]_[PROFILE ENV]_[USER INITIALS (optionnal)]`

```
ISIA_XPROJECT_DEV_GSO
ISIA_XPROJECT_PROD_GSO
ISIA_XPROJECT_ADHOC_GSO

XPROJECT_DEV

COM.ISIA.XPROJECT_PROD
```

**WARNING** : Accent, punctuation, non conventional characters are strictely forbidden !

##Comments
[Back to top](#best-practice-guide)    

Use JSDoc style

####Function documentation

```
/**
 * Represents a book.
 * @constructor
 * @param {string} title - The title of the book.
 * @param {string} author - The author of the book.
 * @return {Book} book - Book object
 */
function Book(title, author) {
 
}

/**
 * Add book.
 * @constructor
 * @param {string} args.title - The title of the book.
 * @param {string} args.author - The author of the book.
 */
 function addBook(args){
  ...
 }
 ```

##Publishing
[Back to top](#best-practice-guide) 

After publishing app on store, don't forget to save following element on **SQT project directory** and / or **GitLab project repository** :

- Android keystore
- Create text file containing _alias_ and _password_ of the keystore
- iOS certificate and provisioning profile
