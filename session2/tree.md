## Trees

What is a tree?
A hierarchical data structure with a root node, and subtrees of children with a parent property. Let's use the DOM as an example...

![simple DOM example](https://snipcademy.com/code/img/tutorials/javascript/dom.svg "Simple DOM")

I know we are all familiar with what the DOM is... that really cool interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document. 

## Let's take a look at how you would implement it...

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

### How is this used?

Let's build it!
For a simple example, let's build the following DOM (yes, a much smaller, simpler version)

// show an image

### How does it look like programmatically?

Well, using our definitions above, we can create the tree like this:

// Here are all of the nodes that we'll need
Node div = new Node("<div");
Node h2 = new Node("<h2>");
Node ul = new Node("<ul>");
Node li1 = new Node("<li>");  
Node li2 = new Node("<li>");  
Node li3 = new Node("<li>");  
Node a = new Node("<a>");
  
// but they need relationships! Let's take care of that here  
// our root "div" has 3 children:
div.children.push(h2);
div.children.push(ul);
div.children.push(a);

// our ul child has 3 children of its own
ul.children.push(li1);
ul.children.push(li2);
ul.children.push(li3);

Awesome! We've written our DOM. Now what?
What's the DOM again? What do we want to do? 
If we want to edit and manage our DOM, we better now how to traverse it.

## What does a tree traversal look like?

Here's an example with recursion and callbacks...

```javascript
  traverse(Node node) {
    Queue q;
    q.push(root);
    breadth_first_recursive(q);
  }
  
  traverse_recursive(callback) {
    // it's empty! we're done
    if q.empty() return;

    // perform our callback on our node
    Node n = q.pop();
    callback(n);
    
    // continue with our children
    node.children.forEach(child => q.push(child));
    traverse_recursive(q);
  }
```

A simple example to traverse the entire tree and print to screen all values:
```javascript
myTree.traverse((node) => console.log(node.data));

// TODO: salmon, mole, 
```
Another way to traverse a tree that scales for large data and illustrates what recursion does would be to **unwind** the recursive function:

```javascript
  traverse(callback) {
  
    const stack = [];
    let node = this.root;
    while (node) {
    
      // evaluate current node
      callback(node);

      // evaluate all children, pushing them to the stack
      node.childred.forEach(child => stack.push(child));
      
      // move to next child in sequence
      node = stack.length === 0 ? null : stack.shift();
    }
  }

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

Because it is so important to quickly access, read, change your DOM tree, on top of being able to traverse the tree, you are also provided with hash tables (dictionaries) of elements by id, to quickly look up specific elements (or nodes) of your tree by index. Hence, why you can use calls like:

```javascript
let object = document.getElementById('myId');
```
or with jQuery:
```javascript
let jQueryObject = $('#myId'); 
```

So when needed, you can also look at combining data structures.
