---
title:  "How does Hoisting Work in Javascript?"
date: 2015-10-29
description: An example-driven lesson on how javascript hoisting works.
---

### What is Hoisting mean anyways?

Before jumping into what hoisting means in the context of javascript, it's important to learn that 'hoisting' simply means to raise something up. What? Here are example usages of the word: She hoisted her backpack onto her shoulders or The tractor hoisted up the fallen tree. The same idea of lifting something up or 'hoisting' something in the natural world also occurs in javascript with variable declarations & function declarations.


### Hoisting in Javascript
There is a conceptual model for how javascript code is interpreted by the browser & that conceptual model is called 'hoisting'. Interestingly enough, if you open up the javascript spec, you will not find the word hoisting anywhere, because hoisting actually isn't a thing. It's a mental construct that we as programmers, particularly in the javascript world, have invented to explain the behavior of javascript.

Let's say we have this file called `file1.js`. Take a look at it for a moment. It looks very simple right?

```js
a;           // ??
b;
var a = 2;   // ??
var b = 2;   // ??
b;           // 2
a;           //???
```

By simply glancing at the code, it would reasonable to assume, that our code would just execute line-by-line, and that variables 'a' & 'b' would cause a reference error, meaning that they weren't defined. What javascript will actually do is go through our entire code first & compile our code before it's executes it. The code you see in `file.js` can more accurately be looked at like this:


```js
var a;   // undefined
var b;   // undefined
a;       // undefined
b;       // undefined
a = b;   // undefined
b = 2;   // b=2
b;       // 2
a;       // undefined
```

Rather than thinking that variable "a" would be undeclared on line 1, in reality in javascript variable declarations get moved to the top of their scope. What's happening is the js engine will go through all of our code & find all of the variable declarations first. Variables get treated first during the compile phase & then the assignments are left in place. This code moving up to the top is what we refer to as hoisting in javascript.


Now, how about with functions? (Before):

```js
var a = b();    //??
var c = d();    //??
a;              //??
c;              //??

function b(){
  return c;     //??
}

var d = function(){
  return b();   //??
}
```



The way it's actually executed (After):

```js
function b(){   // this is function declaration
  return c;
}
var a;          // undefined
var c;          // undefined
var d;          // undefined
a = b();        // a = undefined
c = d();        // c = undefined
a;              // undefined
c;              // undefined
d = function(){ // this is a function expression
  return b();
}
```

Functions get moved to the top first of their scope first, then all of the variables, then code starts executing and then finally variables get assigned their values. Below are some more examples of hoisting.

Hoisting With Nested Scope (Before):

```js
foo();            // ??

function foo() {
  console.log(a); // ??
  var a = 2;
}
```

How the code is actually interpreted (After):

```js
function foo(){
  var a;           // undefined
  console.log(a); // undefined
  a = 2;
}
foo();
```

Another very important aspect of hoisting to learn is that function declarations are hoisted up to the top of their scope, but function expressions are not. For example:

Before:

```js
foo();        //??
var foo = function bar() {
  var a = 1;
  console.log(a)
};
```

After:

```js
var foo;   //undefined
foo();     //trying to invoke undefined is a type error
foo = function(){
  var a;
  a = 1;
  console.log(a);
}
```







<!-- TODO: Correct examples in this section -->
<!--

Hoisting when if statements are involved are also interesting. Note: Javascript version 5 & below don't support block-level scope, only function scope. However, the newest version of javascript does support block scopes when using the keyword "let" instead of var. Tip: avoid declaring non function expressions in these if/else,while, switch blocks etc..

Before:

```js
if (true) {
   function aFunc() { console.log( "a" ); }
}
else {
   function aFunc() { console.log( "b" ); }
}
aFunc(); // what will get logged?
```

What the code actually gets interpreted as (After):

```js
//there is no block scope only function scope for javascript version < 5
function aFunc() { console.log( "a" ); }
function aFunc() { console.log( "b" ); }

if(true){
  function aFunc() { console.log( "a" ); }
} else{
  function aFunc() { console.log( "b" ); }
}
aFunc(); //logs 'b' but we wanted 'a'
```

The fix: don't use function declarations use expressions.

Before:

```js
if (true) {
   var aFunc = function() { console.log( "a" ); }
}
else {
   var aFunc = function() { console.log( "b" ); }
}
aFunc();
```

What the code actually gets interpreted (After):

```js
var aFunc;

if (true) {
   aFunc = function() { console.log( "a" ); }
}
else {
  aFunc = function() { console.log( "b" ); }
}
aFunc(); // logs "a", what we wanted!
```
-->






<!-- TODO: Finish section -->

<!-- Hoisting with precedence involved:
Before:

```js
var a = 1;
function b() {
    a = 10;
    return;
    function a() {}
}
b();
console.log(a);
```

After:

```js
function b() {
  function a() {}
  a = 10;
  return;  
}
var a;
a = 1
b();
console.log(a); //1
``` -->



### Summary:
-  If there are functions(not function expressions), they get hoisted first to the top of the scope in which they were defined in.
-  Next variables are hoisted
-  Afterwards variables are assigned their values.
-  Tip: use function expressions over function declarations, there will be less surprises.


### Additional Resources
- [YDKJS: Scopes & Closures by Kyle Simpson](https://github.com/getify/You-Dont-Know-JS/tree/master/scope%20%26%20closures)
- [Javascript is Sexy : Hoisting](http://javascriptissexy.com/javascript-variable-scope-and-hoisting-explained/)
