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

Without getting too in-depth for the purpose of this article, the pros are in the simplicity as opposed to library/language support needed and the ability to have multiple modules in on file. However it is difficult then to programmatically import modules and dependencies need to be manually managed which is something that we now expect to be resolved for us in the module ecosystem as modern dependencies can be cumbersome.

## CommonJS

CommonJS is a project that aims to define a series of specs to aid development in server side apps. A big focus being modules. The Node implementation of CommonJS is very similiar and draws inspiration from this spec. The general basis of both CommonJS and the Node implementation of modules centres around require and exports. The examples below will focus on Node.

# require
Require is a function that can be used to import bindings/symbols from the exported module to the current scope. Require expects you to pass through the ID of the module as a string, this is the name inside the node_modules directory or the path to it.

~~~javascript
	const importedFn = require('fn');
~~~

# exports
Exports is a unique object that allows you to put any elements in it to get exported together as a publically accessible value, names are preserved qas the key. 

~~~javascript
	module.exports = (arg) => {
		return {
			fn: () => console.log(arg);
		}
	}
~~~

The API works in a synchronous fashion, with the spec being designed in a way that prioritises server-side development. CommonJS in a step up from the revealing module pattern in the sense that dependency management is baked in, as modules which 'require' other modules get loaded in order, synchronously. However this does not make sense client-side where funcitonality and loading does not occur synchronously.

There is a work around to the shortcomings in the browser in the form of webpack and browserify.
Browserify - will bundle code in a single file with dependencies in the right order.
Webpack - Transforms code instead, but will also does some bundling in the modules to solve dependencies on the client.

## Asynchronous Module Definition (AMD)

AMD was created as a direct alternative to CommonJS. The biggest feature that delineates the two, is AMD has base support for asynchronous module loading.

~~~javascript
	define(['dependencyOne', 'dependencyTwo'], function (dependencyOne, dependencyTwo) {
	
	return function () { // do something}
}
~~~

This all works by utilising 'closure', a function is called when the requested modules passed through as the array of dependencies are finished loading. This explicit definition allows the AMD loader to have a full graph of dependencies available to it at runtime. This allows for libraries which do not have depdencies on eahc other to be loaded at the same time. This improves speed at which things become available to the user in the browser/client reducing UX friction. Require.js is a popular library example of this.

## ES2015 Modules

Hooray! This is a standard newly implemented in ES6 as a core feature in the language. The result is a standard that can support both sync/async module operations.

~~~javascript
	/*-------greeter.js---------*/
	const greeting = ' how are you today?';
	export function greeter(name) {
		console.log(name + greeting)
	}
	
	/*-------main.js-----------*/
	import { greeter } from 'greeter';
	greeter('Jas');
	// 'Jas how are you today?'

~~~

The syntax is fairly simple/intuitive - export directive to make the elements of your choice public from your module/import directive to pick and choose the elements you want from the module. Still not supported completely across all clients or natively in Node, but there is work being done towards this and polyfills to assist in the mean time.

One standard will alleviate the overhead needed in keeping up with all these module systems :O
