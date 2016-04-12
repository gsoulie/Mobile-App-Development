#Best practice guide

> **Under construction**

[SASS](#sass)     
[Javascript](#javascript)    
[Ionic 2](#ionic-2)    
[AngularJS 2](#angularjs-2)    
[TypeScript](#typescript)    


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
##Javascript
[Back to top](#best-practice-guide) 

##Ionic 2
[Back to top](#best-practice-guide) 

##AngularJS 2
[Back to top](#best-practice-guide) 

##Typescript
[Back to top](#best-practice-guide)    

[Typescript guideline](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines)
