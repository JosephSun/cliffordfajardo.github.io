---
title:  "JavaScript Libraries Explained"
date:   2015-09-27 10:18:00
description:
---

So you've heard of javaScript libraries such as Underscore, Lodash, and jQuery.
But have you ever wondered how they actually worked behind the scenes? Well, the good news is javaScript libraries aren't so magical after all and you'll see why, soon enough.

### So what is a library anyways?
In programming, a library generally refers to a file(s) full of code that some other
programmer(s) has already made for other developers convenience.

### Why use a library?
In short, libraries make our lives as developers easier and help us get started with our projects
much faster. Other great reasons reasons to use libraries are:

>- generally the code in libraries have been battle-tested in development so you know it's reliable
>- the code has been tested to work across multiple browsers and platforms
>- some library's API (the way you interact with the code) is more user friendly than exisiting native methods
available to you.



### Libraries behind the scenes
Imagine that you downloaded the underscore js library and you've imported it into your
HTML page. Nice, now you have access in your own javaScript file to a bunch of the nice
helper functions inside the underscore library.

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My Amazing Web app</title>

</head>
<body>

  <!-- Importing underscore. This is just a file with prebuilt functions. -->
  <script src="underscore.js"></script>
  <!-- Now I have access inside my javaScript file to underscore's
       function's, since I loaded underscore above my file -->
  <script src="myOwnfile.js"></script>
</body>
</html>
{% endhighlight %}


The eye opening moment for me was when I realized that a lot of libraries store their functionality
inside objects as methods (some libraries vary). One of the reasons why library creators store their
functions inside objects is to avoid creating global variables. By tucking in functions and variables
inside of objects, they only exist inside that object, so you don't have to worry about accidentally
overriding it in your own code.


Lets take a look at the underscore utility library
(I've shortened it and made it simple, as the underscore object contains hundreds of methods inside of it).

{% highlight javascript %}
//underscore.js file
var _ = {};

_.last = function(array){
  return array[array.length - 1];
}
_.flatten = function(array){
  var flattenedArray = [];
  //the code for this function is looong, but imagine it's here
  return flattenedArray;
}
{% endhighlight %}


Remember, since I loaded the underscore.js file first inside my HTML file, I now have
access to underscore's prebuilt functions in my own html file. The best part about
using a library is: not having to compose the functions we use from the library from scratch - yay.


{% highlight javascript %}
//myOwnfile.js

var friends = ['Ann', 'Bob', 'Cal', 'Dan'];
var lastFriend = _.last(friends);  // 'Dan'


var multiNestedArray = [1,2 [3, 4, [5, [6]]];
var flatArray = _.flatten(multiNestedArray); // [1,2,3,4,5,6]
{% endhighlight %}


### Libraries often provide a simple API
Though you can do anything a javaScript library can with your own javaScript,
some of the advantages of using libraries is that they make your code less dense,
often more readable and offer a much more intuitive API's than the native API's
available to you.

{% highlight javascript %}
// *** Vanilla JavaScript using native DOM API ***
// Finding a class(es):
document.getElementByClassName('myClass');
// Finding an ID:
document.getElementById('myID')
// Finding an element(s):
document.getElementByTagName('h1')
//Changing a text on an element with a class of title
var newTitleText = document.getElementByClass('title')[0].nodeValue('hello');



// *** Using jQuery's API ***
/* Somewhere in the jQuery file there is a '$' function with lots of code that we
   didn't have to write. But hey, this $ function does so much with little code!*/
// Finding a class(es):
$('.myTitle')
// Finding an ID:
$('#myID');
//Finding an element(s):
$('h1')
//Changing a text on an element with a class of title
var newTitleText = $('.title')[0].html('hello');


{% endhighlight %}



### When not to consider not using libraries
For the most part, if your application is only needing a few helper functions,
it's perhaps better to create the functions from scratch or find the pure javascript
solutions online, than to bring in an entire library into your project just for two
or three functions that you needed.
