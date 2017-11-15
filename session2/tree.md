## Trees

Let's look at how this data structure can be defined, and then similarly, we'll compare behaviour using our picture album compared to how we saw it behave with the array and linked list.

### Let's define our Node and Tree
```javascript
class Node {
  constructor(value) {
    this.data = value;
    this.parent = null;
    this.children = [];
  }
}
```

```javascript
class Tree {
  constructor(value) {
    this.root = new Node(value);
  }
  
  // functions to edit / manage the tree
  ...
}
```

Of all of the wonderful things we want to do with a tree, we first would need a way to traverse it (visit every node). 

```javascript
// TODO: build a tree
```

// show an image

```javascript
// TODO: switch it to binary tree, show construction and image
```
## What does a tree traversal look like?

Here's an example with recursion and callbacks...

```javascript
  traverse(callback) {
    callback(this.root);

    if (!this.root.children || this.root.children.length < 1) {
      return;
    }
    children.forEach(() => {
      child.traverse(callback);
    });
  }

```

A simple example to traverse the entire tree and print to screen all values:
```javascript
myTree.traverse((node) => console.log(node.data));

// TODO: salmon, mole, 
```

Your callback can be anything here... a function to return all image type children, a counter function to find the number of images, a function that manipulates certain nodes, etc...

What is actually happening in the background, the callback commands are stored in a stack to *remember* what to do *later*... 


## Why use a tree?

Let's go back to our picture album idea, and consider adding pictures in order, as we select additional pictures to add.

Like in the original array and linked list... let's say we still want the pictures in this order:  3, 8, 1, 12 5.
Realistically, they may not be chosen in that order too though. Let's add them to the tree, sorted, as you select them in this order: 1, 3, 8, 12, 5. 
what does our tree look like?

Now what if we selected them in this order with the array or linked list??
+ If we did that with an array, we'd have to shift pictures over to make room for the new picture EVERYTIME we added anywhere but the last position of the array. Lots of copying. NO THANKS!
+ With a linked list, we wouldn't have to copy, but we still iterate through the list linearly, find the spot, ajust a few next pointers. 
+ With a tree, no copying or shifting either, but as we iterate, we are looking through a smaller and smaller subset... it might help to visualize with an album of 100 pictures.

We will take a closer look into sorting and efficiency next time.

+ both insertions (and retrievals) of objects take on the average log2N time, where N is the number of objects stored...
+ the tree naturally grows to hold an arbitrary, unlimited number of objects.


### The DOM

What is the DOM?

It’s an interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document.
It's a great example because you have lots of one-to-many relationships.

![simple DOM example](https://snipcademy.com/code/img/tutorials/javascript/dom.svg "Simple DOM")

Because it is so important to quickly access, read, change your DOM tree, on top of being able to traverse the tree, you are also provided with hash tables (dictionaries) of elements by id, to quickly look up specific elements (or nodes) of your tree by index. Hence, why you can use calls like:

```javascript
let object = document.getElementById('myId');
```
or with jQuery:
```javascript
let jQueryObject = $('#myId'); 
```

So when needed, you can also look at combining data structures.
