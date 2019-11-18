---
title: front-end mastery - event delegation
author: Jordan Binskin
date: '2019-09-28'
categories:
  - front-end
  - javascript
tags:
  - javascript
  - events
---

# Event Delegation

Hi, this article tries to concisely cover event delegation. I've written this for my revision, in the hope it may help your conceptual understanding as well :)

Event delegation is a concept belonging to the DOM (a javascript representation of the document).
    
In this context, event delegation is a mechanism of responding to UI-events via a single common parent in which the event is bound to, as oppose to each individual child elements.

This is made possible by 'event bubbling' a behaviour that causes an event which is triggered on a child node to propagate up the tree in the dom all the way to the root of the document.

The practical use of this mechanism is only needing to attach handlers to the parent as oppose to child nodes. While also not losing reference to the handler if the child node is removed from the DOM. It is cleaner in terms of memory only needing to be bound once, and not needing to attach/remove when element mounts/unmounts DOM.

<hr/>

The example below has an event listener attached to the UL, which has a handler that when one of it's child LI elements are clicked will change that specific LI (courtesy of the event.target property which will specify what node was clicked)text content to be clicked. 

Click item 2 with the console open to see some special behaviour.

~~~html
<ul id="parent-list">
  <li id="post-1">Item 1</li>
  <li id="post-2">Item 2</li>
  <li id="post-3">Item 3</li>
  <li id="post-4">Item 4</li>
  <li id="post-5">Item 5</li>
  <li id="post-6">Item 6</li>
</ul>
~~~

~~~javascript
document.querySelector('ul').addEventListener('click', (e) => {
    if (e.target && e.target.nodeName == "LI") {
     e.target.textContent = "clicked";
    }
    if(e.target.matches('li#post-2')) {
      console.log('Am', event.target)
    }
  })
~~~
