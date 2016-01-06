---
title:  "Data Structures in JavaScript Part 2: Binary Search Tree"
date:   2015-11-21
description: Exploring data structures in javascript
---

## Introduction
This a part one of series of blog posts intended to cover common computer science data structures in JavaScript. Why JavaScript? Frankly, most data structures are taught in Java, C++, Python but seldom in JavaScript.

Links to other posts in series:

- [Stack and Queues](http://cliffordfajardo.github.io/2015/javascript-data-structures-stack-and-queues)
- Tree (coming soon)
- LinkedList (coming soon)
- HashTable (coming soon)
- Sets (Coming soon)

### What is a Binary Search Tree (BST)?
A binary search tree, also known as an ordered binary tree, is a node-based data structure in which each node has no more than two child nodes. Each child must either be a leaf node or the root of another binary search tree.
<img src="http://programminggeeks.com/wp-content/uploads/2014/01/nodes-in-binary-search-tree.png">


Methods:
- search
- insert
- remove



```js
var BST = function(value){
  this.left = null;
  this.right = null;
  this.value = value;
};
```

```js
BST.prototype.insert(value){
  // if(this.value === null) this.value = value;
  var recurse = function(node){
    if(node.value > value){
      if(node.left === null) {
        node.left = new BST(value);
      } else {
        recurse(node.left)
      }
    } else {
      if(node.right === null){
        node.right = new BST(value)
      } else{
        recurse(node.right);
      }
    }
  };
  recurseNode(this);
}
```

```js
BST.prototype.search = function(value){
  var recurse = function(node){
    if(node.value === value) return true;
    if(node.value > value){
      recurse(node.left);
    } else {
      recurse(node.right);
    }
  };
  recurse(this);
  return false;
}
```

```js
BST.prototype.remove = function(value){
  var recurse = function(node){
    if(node.va)
  }
  recurse(this);
}
```


### Additional Resources:
[Iterative Solution & Other Solutions]()
[BST Video](https://www.youtube.com/watch?v=pYT9F8_LFTM)
[More on BST](http://khan4019.github.io/front-end-Interview-Questions/bst.html)
