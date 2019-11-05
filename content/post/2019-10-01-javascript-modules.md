---
title: front-end mastery - amd vs commonjs vs esmodules
author: Jordan Binskin
date: '2019-10-01'
categories:
  - front-end
  - javascript
  - modules
tags:
  - javascript
  - modules
---

# AMD vs CommonJS vs ES2015 Modules.
(Honourable mention to revealing module pattern).

Firstly, why modules in the first place. Modules respect the principles of encapsulation and allow different pieces of software to be developed in isolation or concurrently without having a dependency on it's other pieces until it is time to launch the application.

When bringing these pieces of code together it is important to have the encapsulation that modules provide in order to prevent conflicts between them.

When piecing all the code together the second concern to modules being encapsulated (module scope) is having dependencies satisfied at the right time in the right order, this is implicitly handled in some situations but in others it is on the developer.

These module systems help developers manage both encapsulation and dependency concerns.

## Revealing Module Pattern

Before the 3 modern module solutions, there was a a pattern used independent from these specific API's called 'Revealing Module Pattern', which used function scope to encapsulate data, only allowing methods to get and set these bindings as returned values. This was a pre ES2015 solution where block scope only existed in functions as opposed to let/const bindings in regular blocks.

An example of this is below:

~~~javascript
var bob = function playerModule() { 
  var race = "Orc";
  var classType = "Barbarian";
  
  function changeClass(classUpdate) {
	  classType = classUpdate;
  }

  function getClass() {
    return classType
  }

  function getRace() {
	  return race;
  }

  return {
    getClass,
    getRace: getRace,
    setClass: changeClass
  }
}

bob.getClass()
// "Barbarian"

bob.setClass("Mage")
// undefined

bob.getClass()
// "Mage"
~~~
