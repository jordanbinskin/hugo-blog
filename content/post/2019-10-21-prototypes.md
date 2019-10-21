---
title: front-end mastery - prototypal inheritance
author: Jordan Binskin
date: '2019-09-28'
categories:
  - front-end
  - javascript
tags:
  - javascript
  - object-oriented
  - prototypes
---

# Prototypal inheritance

Prototypal inheritance is one of two main object oriented (OO) paradigms the other being classical inheritance. 

Prototypal inheritance in a straight forward definition is the model in which objects inherit other objects as their prototype (a property on an object that holds reference to an ancestor object).

Prototypical inheritance can be thought as of a chain where objects are connected to one an other. This allows behaviour to be shared/ or delegated. If same properties exist in an object as its own prototype, precedence is given to the object in which the property is being accessed and then each step up the tree. (searching up the prototypal tree is a common phrase describing this.)

The way JavaScript does OO is based off the Prototypal model. There is what developers refer to as ES6 'syntax sugar' that lets you write code that looks like classical inheritance but is same old prototypal inheritance underneath.

<hr/>

In prototypal OO languages, everything is an object. Meaning there is only one 'type' of abstraction, that being an object. Every other 'thing' inherits from the single Object prototype. 

Meaning in terms of classic OO terms, everything is either abstracting a real word entity, i.e. a subaru object, or a car object which describes/abstracts the subaru object and acts as its prototype and is a generalization of the subaru.

***2 main pros***

1. There is only one type of abstraction (the might Object).
2. Generalizations are simple objects (that abstract other objects).


Some general useful OO terms:

- ***Abstraction:*** A way of representing real 'things' in compute r programs. More accurately a general concept formed by extracting common features of a specific example.

- ***Generalization:*** An abstraction of a more specific abstraction.

~~~javascript
const everything = Object.create();
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
