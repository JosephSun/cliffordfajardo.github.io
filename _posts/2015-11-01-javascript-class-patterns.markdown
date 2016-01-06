---
title:  "JavaScript Class/Instantiation Patterns"
description: Exploring different class patterns in JavaScript through examples
date: 2015-10-4
---

Like in pretty much all things in life, *there are several ways you do things*.
However, sometimes it's worth exploring which solutions are popular, efficient, readable or what have you. Over the past few months as I've been deep diving into javascript. I've come across several ways you can create "classes" in the language. I recall the frustration I had when I first started learning about this topic, so today I'd like to briefly share with you the different class instantiation I've learned.


###Functional Pattern

{% highlight javascript %}
var Car = function(color){
  var obj = {};
  obj.color = color;
  obj.door = 'closed';
  obj.doorOpen = function(){
    obj.door = "open";
  };
  obj.closeDoor = function(){
    obj.door = 'closed';
  };
  return obj;
};


var car = Car('red');
{% endhighlight %}

Pros:

- clear object construction
- everything that is being done is contained inside the function


Cons:

- Methods duplicated for every object we create, so new spot in memory created.
- Not ideal if your creating multiple instance of objects.





###Functional shared pattern
{% highlight javascript %}
//Functional-shared pattern
var Car = function(color){
  var obj = {};
  obj.color = color;
  obj.door = 'closed';
  obj.openDoor = carMethods.openDoor;
  obj.closeDoor = carMethods.closeDoor;
  return obj;
};


var carMethods = {};
carMethods.openDoor = function(){
  this.door = 'open';
};
carMethods.closeDoor = function(){
  this.door = "closed";
};

var car = Car('red');
{% endhighlight %}


Pros:

- clear object construction
- no duplication of methods each time we create an instance


Cons:

- Setting method pointer is less efficient than delegating a fallback
- Not ideal, if your creating multiple instances of objects.










###Prototypal Pattern
{% highlight javascript %}
var Car = function(color){
  var obj = Object.create(Car.prototype);
  obj.color = "color";
  obj.door = 'open';
  return obj;
};

//Automatically created by interpreter
//Car.prototype = {};
Car.prototype.openDoor = function(){
  this.door = 'open';
};
Car.prototype.closeDoor = function(){
  this.door = 'closed';
};

var car = Car('red');
{% endhighlight %}


Pros:

- clear object construction
- no duplication of methods each time we create an instance


Cons:

- Setting method pointer is less efficient than delegating a fallback
- Not ideal, if your creating multiple instances of objects.








###Pseudoclassical Pattern
{% highlight javascript %}
var Car = function(color){
  //Automatically created by interpreter
  //var this = Object.create(Car.prototype);
  this.color = color;
  this.door = 'open';

  //return this;
};

var car = new Car('red');
{% endhighlight %}




###ES6 Class keyword
{% highlight javascript %}
class Car {
  constructor(color){
    this.color = color;
  }
  openDoor(){
    this.door = 'open';
  }
  closeDoor(){
    this.door = 'closed';
  }
}
var car = new Car('red');
{% endhighlight %}

The ES6 class pattern is still relatively new, and there's still a lot of debate on whether to use this or the other patterns like the prototypal and pseudoclassical pattern.


###Resources
- [Class Patterns infographic - thanks Ryan](http://i.imgur.com/0K5Sgze.png)
- [Intro to ES6 Classes](http://ilikekillnerds.com/2015/02/a-guide-to-es6-classes/)
