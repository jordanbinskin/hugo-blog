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

Firstly, why modules in the first place. Modules respect the principles of encapsulation and allow different pieces of software to be developed in isolation or concurrently without having a dependency on it's other pieces until i's time to launch the application.

When bringing these pieces of code together it is important to have the encapsulation that modules provide in order to prevent conflicts between them.

When piecing all the code together the second concern to modules being encapsulated (module scope) is having dependencies satisfied at the right time in the right order, this is implicitly handled in some situations but in others it is on the developer.

These module systems help developers manage both encapsulation and depedency concerns.

## Revealing Module Pattern

--- to be finished.


~~~javascript
const everything = {};
const livingBeing = Object.create(everything);
const adam = Object.create(livingBeing);

everything.name = 'everything';
livingBeing.name = 'living being';
adam.name = 'adam';

everything.greet = () => 'i am everything';

// Prototypal tree of "Adam"
// { adam } <- { livingBeing } <- { everything }

adam.name
// 'adam'
livingBeing.name
// 'living being'
adam.greeting()
// 'i am everything'
~~~
