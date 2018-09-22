---
layout: post
title:      "An Introduction to Javascript Scope, Hoisting & Context"
date:       2018-09-22 01:34:23 -0400
permalink:  an_introduction_to_javascript_scope_hoisting_and_context
---


What is Hoisting?

In Javascript, hoisting moves a variable to the top of the current scope or current function.

A variable can be declared before it is used:

```
var x; // declares the variable x and hoists it but it will be undefined until it is assigned a value.
undefined
console.log(x);
undefined
```

A variable can be declared after it is used:

```
x = 100;

console.log(x);
100

var x; 

console.log(x);
100
```

What is "scope" in JS?

There are 2 scopes in Javascript: 

Global

A global variable is declared outside of a function and can be accessed everywhere.

```
Var x = 5;

Function printX() {
      Console.log(x);
}

//this will print 5
```
 
Local

A variable declared inside a function is local.  It’s scope is local to the function, which means it 
can only be called in the function it is declared.

```
Function localVar() {
      var y = 6;
}

y;  // calling y outside of the function will be undefined
```

What is "context" in JS?  How/when does the keyword `this` receive its value?

In the global context, “this” is equal to the window object.

```
var x = 5;

console.log(this.x); // returns 5  
```

If you are calling an object value, you call it like this:


```
object = {
    x: 5
};

object.x // returns 5


//If you were calling x from a function inside the object, it would be this.x
```


How do ES6 syntaxes such as `let` and `const` affect hoisting and scope, compared to `var`?

Let and const are different from var in that they are not hoisted.  You can define the same variable as in the global scope inside a function with let without it overriding the original value.  It is the same with const, except that the value inside the function can only be defined once.  

```
var x = 5

function test() {
   let x = 6 ;
   console.log(x); // 6
}

console.log(x); // 5 
```

How does ES6 arrow function syntax affect context (`this`)?

`this` always refers to the scope in which the function was created in.  

For example, if it is created in the global scope, that is the scope of the arrow function.

```
var x = (() => this);

x(); === window // will return true.
```





