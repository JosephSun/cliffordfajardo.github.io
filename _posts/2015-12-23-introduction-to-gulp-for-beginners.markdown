---
title:  "Introduction to Gulp JS"
description: "A step by step tutorial for beginners learning Gulp on Mac"
## date: 2015-12-23
---


![Gulp-logo](/assets/images/posts/00gulp-logo.png)


As Front-end developers we are often told to do a lot of things such as:

>- **Minify CSS and Javascript** to make their file sizes small for our production website.
>- **Compress our images** to reduce their size to help increase page load times.
>- **Use Sass** for CSS because it helps us right write maintainable CSS
>- **Break our CSS and JavaScript into smaller modules** then concatenate them together for the production website.
>- and the list goes on ....


Doing all of those tasks manually can be cumbersome. Let me introduce you to Gulp.js - a task runner - than can do all of the aforementioned tasks and more for you!



## Prerequisites
Before we install Gulp we need to make sure we have Node.js and NPM installed on our system. To check if you have Node installed, simply open your terminal application and enter `node -v`. If you don't have Node installed, we'll need to install to other applications on our Mac -- Xcode and Homebrew. Installing these two applications should only take a few minutes. To install these two applications I highly recommend you check out this short reading called ["How to Install Node.js and NPM on a Mac"](http://blog.teamtreehouse.com/install-node-js-npm-mac).



##Getting started with Gulp
To help you get started with Gulp, I've created a project folder you can download [here](https://github.com/cliffordfajardo/gulp-tutorial/archive/master.zip) that you can use to follow along with this tutorial. Now that you have the **my-website** folder downloaded, let's begin!


###Getting Grunt installed
In your terminal, inside the root of our **my-website folder**, we'll need to run `npm init` to get our project started. Next, your terminal will prompt you to answer a few questions. You can leave them blank if you want, it won't matter for this tutorial.
Now, if you look into your folder, you should have a package.json file.

![After npm init](/assets/images/posts/01gulp-json-file.png)


Next, we want to run the next two commands in our terminal:
{% highlight bash %}
npm install -g gulp
{% endhighlight %}
{% highlight bash %}
npm install gulp --save-dev
{% endhighlight %}

We just told to install gulp globally and to add it to our project's development dependencies. Dependencies lets developers know which node modules should be installed with your project.


Now in if you look inside your package.json file, you should see something like this:
{% highlight json %}
{
  "name": "my-website",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "gulp": "^3.9.0"
  }
}
{% endhighlight %}

**NOTE:** everytime you install a new package (like we did with gulp), your package.json's dependencies list will be updated.


Lastly, we'll need to create a filed called **gulpfile.js**  in our project root. This file will contain the instructions we want gulp to do.

##A Getting started with Gulp
To use Gulp you just need to know four things:

>- gulp.task
>- gulp.src
>- gulp.dest
>- gulp.watch

`gulp.task` defines your task. Its arguments are *name* (your task name), *deps* (optional) and *fn* (the function that does your task). Here is an example:

{% highlight javascript %}
gulp.task('mytask', function() {
  console.log('gulp is running');
});
{% endhighlight %}

`gulp.src` points to the files we want to use. It uses `.pipe` for connecting it’s output into other plugins.

`gulp.dest` points to the destination folder we want to write files to. Here is a simple example of `gulp.src` and `gulp.dest` in action:

{% highlight javascript %}
gulp.task('copyJS', function() {
  // copy any js files in source to our production folder
  gulp.src('source/*.js')
  .pipe(gulp.dest('production')); //<--- this is relative to our gulp file which is in the root.
});
{% endhighlight %}


##Creating our first task with gulp
For our first task we'll simply log to our console that Gulp is running. Inside your **gulpfile.js** we'll put:


{% highlight javascript %}
//Here we're loading the gulp module
var gulp = require('gulp');

//creating our task named test
gulp.task('test', function(){
  console.log("Gulp is running");
})

{% endhighlight %}

Now to run our task we'll go to our projects root in the terminal and type gulp and the name of the task we want to run like this:

{% highlight bash %}
gulp test
{% endhighlight %}

If all went well you should see something like this in your terminal:
{% highlight javascript %}
[09:50:00] Using gulpfile ~/Projects/my-website/gulpfile.js
[09:50:00] Starting 'test'...
Gulp is running
[09:50:00] Finished 'test' after 165 μs
{% endhighlight %}

Great, you've now created your first gulp task now lets concatenate our CSS our JavaScript files:

###Concatening files javascript files
Now we're going to merge all of our javaScript files into just one file for production. First we'll need to install a package called `gulp-concat`. So in your terminal run `npm install gulp-concat --save-dev`. Now your package.json's dependencies should have gulp-concat. Now let's update our **gulpfile.js**.

{% highlight javascript %}
var gulp = require('gulp'),
  concat = require('gulp-concat'); //loading new plugin

//Task: Concat javascript
gulp.task('concatScripts', function(){
  gulp.src([  //telling gulp where our files live relative to gulpfile.js
    'js/jquery.js',
     'js/main.js'
  ])
  .pipe(concat("app.js")) // the output file
  .pipe(gulp.dest('js'))  // new file will go to our js folder

});
{% endhighlight %}

Now in your terminal run the new task we created:

{% highlight javascript %}
gulp concatScripts
{% endhighlight %}

If all went well, you should see a new file in your **js** folder called **app.js**. If you take a look inside of it you'll see we have one big javaScript file. Success!!



###Minifiying javascript files
To minify our javaScript, we'll need to install a new package called `gulp-uglify`. So in your terminal run `npm install gulp-uglify --save-dev`. Now let's update our **gulpfile.js** to add our new gulp task:



{% highlight javascript %}
var gulp = require('gulp'),
  concat = require('gulp-concat'),
  uglify = require('gulp-uglify'); //loading new plugin

//Task: Concat javacript files
gulp.task('concatScripts', function(){
  gulp.src([  
    'js/jquery.js',
     'js/main.js'
  ])
  .pipe(concat("app.js"))
  .pipe(gulp.dest('js'))
});

//Task: Minify javascript file
gulp.task('minifyScript', function(){
  gulp.src('js/app.js')
  .pipe(uglify())
  .pipe(gulp.dest('js'));
})
{% endhighlight %}


Nice. Now if you look at **app.js** we have a minified file, but what if I need to go debug the code we wrote. O wait, we just minified the file and now it looks like gibberish. What we should have done was have our minified code be outputted to a new file which we would use for production. Let's call that file app.min.js. Lets go back to the terminal and install our new plugin: npm-install gulp-rename --save-dev. Next, we'll include the new plugin in **gulpfile.js**.


{% highlight javascript %}
var gulp = require('gulp'),
  concat = require('gulp-concat'),
  uglify = require('gulp-uglify'),
  rename = require('gulp-rename'); //loading new plugin

//Task: Concat javascript files
gulp.task('concatScripts', function(){
  gulp.src([  
    'js/jquery.js',
     'js/main.js'
  ])
  .pipe(concat("app.js"))
  .pipe(gulp.dest('js'))
});

//Task: Minify javascript file
gulp.task('minifyScript', function(){
  gulp.src('js/app.js')
  .pipe(uglify())
  .pipe(rename('app.min.js')) //piping uglify to rename
  .pipe(gulp.dest('js'));
})
{% endhighlight %}

To get our **app.js** back to it's unminified form, let's run in our terminal: `gulp concatScripts`. This is going to overwrite the minified app.js with the concated version. Next, lets run the new minifyScipt task with the newly added rename plugin by running `minifyScript`. Now if you look in your **js** folder, you should see the **app.min.js**





###Turn Sass into CSS, automatically
Now, lets start compiling our Sass to CSS! Let's install our new plugin: `npm install gulp-sass --save-dev` and lets modify our **gulpfile.js**.

{% highlight javascript %}
var gulp = require('gulp'),
  concat = require('gulp-concat'),
  uglify = require('gulp-uglify'),
  rename = require('gulp-rename'),
  sass   = require('gulp-sass'); //loading new plugin

  //........previous tasks....


  //Task: Compile Sass to CSS
  gulp.task('compileSass', function(){
    gulp.src("scss/main.scss")
    .pipe(sass().on('error', sass.logError))
    .pipe(gulp.dest('css'))  delete css folder to see if it works
  })

{% endhighlight %}

To check if our plugin works, let's delete our css folder and then run `gulp compileSass'. You now should have a css folder with file called **main.css**.


### Automating the Repettive Tasks
Great, we've learned how to set up Gulp, but now let's set it up to run our tasks everytime our file changes.

{% highlight javascript %}
//Watch task
gulp.task('watch',function() {
    //anytime of our sass files change, compile!
    gulp.watch('scss/**/*.scss',['compileSass']);
    //anytime our js files change, run concat and minifyScript tasks!
    gulp.watch('js/**.js', ['concatScripts', 'minifyScript']);
});

//Gulp default task
gulp.task('default', ['watch'])
{% endhighlight %}

This last task is very simple, we use the `.watch()` method. We pass in the path to the files we want to watch, and then pass in an array with the tasks that we want to run when the files are changed. The great thing about this task is since we have called this task ‘default’, we can just run `gulp` when we want to run gulp, no need to specify a task! And it will now just sit and wait for files to be saved and then run our task!


### Gulp resources:
- [Gulp video playlist](https://www.youtube.com/playlist?list=PLv1YUP7gO_viROuRcGsDCNM-FUVgMYb_G)
