#Best practice guide

> **Under construction**

[SASS](#sass)     
[Javascript](#javascript)    
[Ionic 2](#ionic-2)    
[AngularJS 2](#angularjs-2)    
[TypeScript](#typescript)    
[Commit](#commit)    


##Sass
[Back to top](#best-practice-guide) 

[Sass best practice documentation](https://sass-guidelin.es/fr/#syntaxe--formatage)

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

[Typescript guideline](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines)

##Commit
[Back to top](#best-practice-guide)    

**<page>** **<element>** **:** **<description/ticket number>**


