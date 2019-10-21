---
title: front-end mastery - 'this' keyword
author: Jordan Binskin
date: '2019-09-14'
categories:
  - front-end
  - javascript
tags:
  - javascript
---

# Event Delegation

'this' is a keyword in JavaScript, which returns a reference to an object or undefined. It is implemented in many
programming languages. However its behaviour in JavaScript varies compared to other languages, mainly where 'this'
is called.

'this' in Javascript is determined by when it is called, in an order of precedence.

1. 'new' Keyword - If the invoked function is called using the new keyword then this will refer to the newly
instantiated object.

~~~javascript
function ConstructorExample() {
  console.log(this);
  this.value = 10;
  console.log(this);
}
new ConstructorExample();
// -> {}
// -> { value: 10 }
~~~

2. If the methods belonging to the function prototype, apply, call or bind are called, then 'this' in the context of the function becomes the argument supplied to these function methods.

~~~javascript
function fn() {
  console.log(this);
}

var obj = {
  value: 5
};

var boundFn = fn.bind(obj);
boundFn();     // -> { value: 5 }
fn.call(obj);  // -> { value: 5 }
fn.apply(obj); // -> { value: 5 }
~~~

side note, bind will create a new function with the properties provided in the function call. While apply and call does not create a new function, it merely will invoke the function with the properties belonging to this
immediately, apply takes an array while call will take the arguments separately listed out.

3. So, outside of the methods mentioned above - when a method is called on an object then this will be the value of this will be the object to the left of the dot.

~~~javascript
var obj = {
  value: 5,
  printThis: function() {
    console.log(this);
  }
}

obj.printThis(); // -> { value: 5, printThis: ƒ }
~~~

4. If a function was freely invoked on its own, referred to as a free function invocation. Meaning it was invoked without any of the conditions above (without 'new', as a function prototype method, or as a method belonging to an object) then 'this' will be the global object. In a browser, this is the 'window'. Or inside another object it is that global object.

~~~javascript
function fn() {
  console.log(this);
}
// If called in browser:
fn(); // -> Window {stop: ƒ, open: ƒ, alert: ƒ, ...}
~~~

***The highest rule in this list wins.***
- Enter the arrow function!!! () => "PYAH". The arrow function does not care where it is called, rather the surrounding scope of where it is created/declared.

~~~javascript
const obj = {
  value: 'abc',
  createArrowFn: function() {
      return () => console.log(this);
  }
};
const arrowFn = obj.createArrowFn();
arrowFn(); // -> { value: 'abc', createArrowFn: ƒ }
~~~