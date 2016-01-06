---
title:  "What is Time Complexity & Why is it Important?"
date: 2015-12-14
description: A brief introduction of time complexity and Big-O with examples for software engineers and new programmers.
---

Time complexity. I remember the first time I heard those words and thought "yikes, that's sounds complicated".
Fortunately, time complexity isn't as difficult to understand as the word makes it seem. In this blog post,
I hope to explain with examples just enough about time complexity to help you start thinking about your
code in a new way and shed light on the importance time complexity has in software engineering.

### What is Time Complexity / Big-O Notation?
Time complexity simply refers to the worst-case scenario of how slow our code could be running at. Also, when talking about time complexity, you might also hear the term Big O or Big O notation thrown which refers to a specific measure of how long are code takes to run. You might here an engineer say "I just optimized my quadratic time function to run at linear time." Here are some of types of the Big-O notations we'll be learning about (which are also the most common):

- **O(1)**  ----- Constant time
- **O(n)**  ----- Linear time
- **O(log n)** - Logarithmic time
- **O(n^2)**  -- Quadratic time

### Why is time complexity important?
Learning about time complexity helps us better understand and improve the efficiency of our code. The efficiency of our code becomes extremely important when you are shipping code that users of your product rely on. To put time complexity into context, Google has calculated that if it's search results slowed down by just 1/4 of a second (think time complexity), it would lose about 8 million searches a day!

Lets review time complexity:

### Constant time: O(1)
an operation is said to be in constant time if it's time execution always stays the
same no matter the input size. Examples of constant time operations:

```js
//Accessing a value in a array or object by it's key no matter the size

var smallList = [1,2,3,4];
smallList[3]  // returns 4 in constant time

var bigList = {1:"anne", 2:"ben", ... 500:"laura"};
numbers[500]  // returns laura in constant time



//Whats the time complexity of running this function? (See invocation times below)
function squareEachNumber(array) {
  for (var i = 0; i < 3; i++) {
    array[i] = array[i] * array[i];
  }
  return array;
}

//Answer: Constant time, since we are only iterating 3 times no matter the input size
squareEachNumber([1,2,3,4,5]);
squareEachNumber([1,2,...,500]);
```


### Linear time: O(n)
an operation is said to be in linear time if it's time execution is directly proportional
to input size. Examples of linear time operations:

```js
var smallList  = [1,2,3];
var mediumList = [1,2,3,4,5,6,7]
var bigList    = [1,2...,500];

//What is the time complexity of running this function? (see invocation times below)
function loopTheList(list){
  var numberOfIterations = 0;
  for(var i = 0; i < list.length; i++){
    numberOfIterations += 1;
  }
  return numberOfIterations;
}
//Answer: linear time
loopTheList(smallList);  // 4
loopTheList(mediumList); // 7
loopTheList(bigList);    // 500


//What is the time complexity of running this loop?
//Answer: linear time
var n = 100
for(var i = 0; i < n; i++){
  console.log(i)
}
```


### Logarithmic: O(log n)
an operation is said to run in logarithmic time if the time execution grows at a rate less than
linear. Here is an example of logarithmic time:

```js
//This function divides the number by 2 every iteration of the while-loop
function logarithmic(number){
  var numberOfIterations = 0;
  while( number > 1){
    number = number / 2;
    numberOfIterations += 1;
  }
  return numberOfIterations;
}
//Notice how the execution time is growing at a rate less than linear.
logarithmic(20);    // 5
logarithmic(30);    // 5
logarithmic(40);    // 6
logarithmic(500);   // 9
logarithmic(1000);  //10
```


### Quadratic time: O(n^2)
an operation is said to run in quadratic time if the time execution is
directly proportional to the square of the input size.

```js
var list = [1,2,3];
duplicateTheList(list);

//quadratic time function
function duplicateTheList(list) {
  var duplicate = [];
  //iterate over each element in list
  for (var i = 0; i < list.length; i++) {
    duplicate[i] = [];
    //after creating a new array above,
    //insert every item in the list into it.
    for (var j = 0; j < list.length; j++) {
      duplicate[i].push(list[j]);
    }
  }
  return duplicate;
}
//input = 3
[1,2,3]
//output = 9
[ [ 1, 2, 3 ], [ 1, 2, 3 ], [ 1, 2, 3 ] ]

/*
For every iteration of the outer for-loop there are 3 operations that take place inside:
When i is 0, the inner for loop will run 3 operations inside, then i becomes 1
When i is 1, the inner for loop will run 3 operations inside, then i becomes 2
When i is 2, the inner for loop will run 3 operations inside, then i becomes 3 and we stop
*/
```

### Additional Resources:

- [Big O Cheat Sheet](http://bigocheatsheet.com/)
- [Time Complexity by Codality](https://codility.com)
