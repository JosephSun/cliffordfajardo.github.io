---
title:  "NPM Essentials"
description: What you need to know about NPM
## date: 2015-10-1
---


### Intro to NPM

NPM is a command line drive package manager for JavaScript. It's a great way to easily
install tools and include other people's code in your projects. NPM is used by hundreds of thousands of web developers today. Companies like Google, Facebook, small companies and just about any experienced web developer is using it today. To browse packages on NPM you can go their main website [npmjs.com](https://www.npmjs.com/)


### Installing Packages
There are two ways methods of installing a NPM package on your computer. They are:

- **installing local packages**: this means the package you are installing is local to your project. Example of applications I usually install locally are libraries like: lodash and jQuery.I don't need these to live on my computer, when I need them I'll fetch them online since they are small.

- **installing global packages**: this means the package you are installing is saved on your computer and you can use the package's tools directly from the command line (if they are available). Examples of apps that I have installed globally are: Sass, Gulp and http-server. I use these tools from my command line all of the time so they live on my computer.


###Where your Packages Live:
To find where your **global packages** live on Mac you can run the following command: `npm list -g --depth=0`. When you run this command you should see something like outputted to your terminal:

{% highlight bash %}
/usr/local/lib
├── bower@1.4.1
├── generator-test@2.0.2
├── gulp@3.9.0
├── http-server@0.8.5
├── npm@3.3.4
├── recess@1.1.9
├── talentbuddy@0.0.16
└── yo@1.4.8
{% endhighlight  %}

To list all of your **local packages** you just need to into our **node_modules** folder and you'll see all of the packages in there.


###More to come:
Later I'd like to come back and explain the confusing parts of NPM like:

- [devDepenencies, dependencies and local dependencies](http://stackoverflow.com/questions/18875674/whats-the-difference-between-dependencies-devdependencies-and-peerdependencies)
- updating npm packages
- [here's a cool npm visualization](https://unpm.nodesource.com/)
