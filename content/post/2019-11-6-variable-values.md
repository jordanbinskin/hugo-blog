---
title: front-end mastery - null vs undefined vs undeclared
author: Jordan Binskin
date: '2019-11-04'
categories:
  - front-end
  - javascript
tags:
  - javascript
  - variables
  - types
---

## JavaScript Quirks: undeclared, undefined or null?

In JavaScript there is more than one way to refer to an 'nothing' value. First, there are two types of variables (or bindings) those which you have declared, and those which you have not. 

~~~javascript
  var thing;

  console.log(thing);
  // undefined

  console.log(stuff);
  // Reference error: undeclared.
~~~

I have now declared *thing*, which returns a value of undefined. While *stuff* has not been declared, hence the JavaScript runtime will give us an error message as our variable does not exist (is undeclared).

The next thing you can do after you declare a variable, is assign it a value. You can shortcut declaring a variable and go straight to its assignment. This is highly unrecommended, without much nuance to argue the other way. 






