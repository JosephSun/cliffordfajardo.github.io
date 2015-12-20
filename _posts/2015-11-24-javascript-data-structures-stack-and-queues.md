---
title:  "Data Structures in JavaScript Part 1: Stack & Queues"
date:   2015-09-27 10:18:00
description: Exploring data structures in javascript
---

## Introduction
This a part one of series of blog posts intended to cover common computer science data structures in JavaScript. Why JavaScript? Frankly, most data structures are taught in Java, C++, Python but seldom in JavaScript.

- Stack and Queues
- Tree (coming soon)
- Binary Search Tree (coming soon)
- LinkedList (coming soon)
- HashTable (coming soon)
- Sets (Coming soon)

We're first going to start by reviewing stacks and then transition into Queues.


### What is a Stack?
A Stack is data structure where insertion and deletion of items take place on one end called top of the stack. An easy acronym to help you remember Stacks insertion and deletion rule is LIFO (Last in First Out). Another way of thinking about stacks is like a stack of papers, you add to end(top) of the stack and remove from the top.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/29/Data_stack.svg/391px-Data_stack.svg.png"/>

Before we jump into implementing a stack from scratch let's take a look at how javaScript's arrays can serve as stacks, and we'll use this example as our mental model for our own implementation:

```js
var myArray = [];
myArray.push(1,2,3); // [1,2,3]
myArray.pop();       // [1,2]
```

By definition, javaScript's array can serve as stack since it has the ability to insert and remove items at the size or top
of the stack. Why learn how to create our own stack? Well, some programming languages don't have arrays or lists, and also its
a great learning experience! Note: using [pseudoclassical](http://www.ryanatkinson.io/javascript-instantiation-patterns/) class pattern for this algorithm.

Lets implement our own stack data structure in JavaScript. Yes, we will be creating our own implementation of an array! Hopefully this sounds interesting to you and if it does, you’re in for a treat!

### Defining the Problem
As we've discussed a stack is data structure for storing items. We'll need a method for pushing items into the stack (push)  ,removing the last item(pop) from the stack and a method that returns to us the size of the Stack.

- push
- pop
- size


```js
//Defining our stack class
var Stack = function() {
  this.size = 0;      // tracks stack count & is the key for last item to pop in storage
  this.storage = {}; //  where items will be stored
};
```

```js
Stack.prototype.size = function(){
  return this.size;
};
```

Every time we push a new value into the stack, we set the key for that value in storage to be the value of size.
Then we increment the size value after adding. For example, if we push the first time with 0, we'll have `this.storage[0] = 0`, the second time with one would be `this.storage[1] = 1`

```js
Stack.prototype.push = function(value){
  this.storage[this.size] = value;
  this.size++;
};
```

When removing items from the stack, we only want to pop if the stack is not empty. Also given that our size value
will always be one value of the highest index in our storage, we immediately decrement size before deleting.

```js
Stack.prototype.pop = function(){
  if(this.size() > 0){
    this.size--;
    var poppedItem = this.storage[this.size];
    delete this.storage[this.size];
    return poppedItem;
  }
};
```

### Trying out our Stack:

```js
var myStack = new Stack();
myStack.push(1);   // {0:1}
myStack.push(2);   // {0:1, 1:2}
myStack.size();    // 2
myStack.pop();    //  stack is now {0:1}
```

<br><br><br><br></br>

### What is a Queue?
A Queue is a data structure where insertion of items take place at the top and deletion of items take place from the bottom of the queue. FIFO (First in First Out). Another way to think of a Queue is like a line at movies. Customers come in and they are only served if they are first.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/300px-Data_Queue.svg.png">

Before we jump into implementing a Queue from scratch let's take a look at how javaScript's arrays can serve as queues, and we'll use this example as our mental model for our own implementation:

```js
var myArray = [];
myArray.push(1,2,3); // [1,2,3]
myArray.shift();     // array is now [2]
```



### Defining the Problem
As we've discussed a queue is data structure for storing items. We'll need methods for pushing items into the queue (enqueue),removing the first item (dequeue) and a method that returns to us the size of the Queue.
- enqueue
- dequeue
- size


```js
//Queue class
var Queue = function(){
  this.start = 0;       // keeps track of the first item's index
  this.end = 0;         
  this.storage = {};    // where items will be stored
};
```


Our queues enqueue method is identical to our stacks push method - they are both just adding items.

```js
Queue.prototype.enqueue = function(value){
  this.storage[this.end] = value;
  this.end++;
}
```

```js
Queue.prototype.dequeue = function(){
  if(this.size() > 0){
    var dequeuedItem = this.storage[this.start];
    delete this.storage[this.start]
    this.start++; //every time we delete, update start to point to new first index
    return dequeuedItem;
  }
};
```

```js
Queue.prototype.size = function(){
  return this.end - this.start;
};
```

### Trying out our Queue:

Enqueuing:

```js
var myQueue = new Queue();
myQueue.enqueue(0);  // {0:0}
myQueue.enqueue(1);  // {0:0, 1:1}

// At this point in time our queue and variables are:
// start = 0 , end = 2
{ 0:0, 1:1 }
```

Dequeuing:

```js

//Before our dequeue:
// start = 0 , end = 2
{ 0:0, 1:1 }

myQueue.dequeue();   
//After our dequeue:
//start = 1, end = 2
{1: 1}
```

Getting the size:

```js
//queue at this time:
//start = 1, end = 2
{1: 1}

myQueue.size()
//recall size is end - start -----> 2-1 = 1
```
