---
title: front-end mastery - array helpers
author: Jordan Binskin
date: '2019-11-19'
categories:
  - javascript
tags:
  - arrays
  - javascript
---

# Array helper methods

With the increased popularity of 'functional' programming, which pushes a more 'declarative' style of programming (describing what you're doing - hiding the nitty gritty) and avoiding mutating the state of your program the Array helper methods have grown in usage too.

Each method could get an article of its own, so this article will cover more of the 'why' use one over the other when working with arrays. I'll slip through some MDN links for more reference until then.

All of these assume you have an array and you want to do something with it. These methods belong to the Array prototype, so can be called as a method of the array as with filter below:

~~~javascript
  let someArray = [1, 2, 3];
  let odds = someArray.filter((num) => num % 2 !== 0)
  console.log(odds)
  // [1, 3]
~~~

## forEach
Why? You have an array and you want to do something 'for each' item without returning a new array. This mean forEach is mainly used for producing 'side effects', and if following a functional paradigm should not be used for mutating an existing array.

An example of using a forEach could be wanting to log the value of array item.

~~~javascript
  let names = ['Billy', 'Scott', 'Sandra'];
  names.forEach((name) => console.log(name));
  // Billy
  // Scott
  // Sandra
~~~

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach

## filter
Why? You have an array and you want to return a new one that removes the items you don't need. The first example used a filter to remove even numbers, let's do another one for good practise.

An API has returned an array with pesky commas in it that I don't need.. hmm let's see..

~~~javascript
  let raw = ["Table", ",", "Chair", ",", "Fridge"];
  let clean = raw.filter((item) => item !== ",");
  console.log(clean);
  ["Table", "Chair", "Fridge"];
~~~

Voila, clean data for the rest of the app.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter

## map
Why? You have an array and you want to transform each item and place them in a new array to use.

I want to capitalise each letter in this string array.

~~~javascript
  let lowercase = ["s", "a", "h"];
  let upperCase = lowercase.map((item) => item.toUpperCase())
  console.log(upperCase);
  // ["S","A","H"]
~~~

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map

## reduce
Why? You have an array and you want to represent it as a single value or have a question about it that could be summed up in a single value (these can also include complex data types, but more often a single value).

Taking inventory of the pets. How many dogs do we have?

~~~javascript
  let pets = ["dog", "cat", "dog", "dog", "cat"];
  let numberOfDogs = pets.reduce((count, pet) => {
    if (pet == "dog") count++;
    return count;
  }, 0)
  console.log(numberOfDogs)
  // 3
~~~

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce