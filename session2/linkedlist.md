# Linked List

In order to introduce linked lists, we are first going to solve a problem using arrays and go from there...



## Quick recap: Two ways of creating your array and adding to your array

We are discussing here the data structure, array. Not the JavaScript Array.

### 1) I initialize the size of the array with some room to grow

```javascript
let largeAlbum = new array(50); 
largeAlbum[0] = 3;
largeAlbum[1] = 8;
largeAlbum[2] = 1;
largeAlbum[3] = 12;
largeAlbum[4] = 5;
```

Now what if I want to add a new picture to the array? No problem.

```javascript
largeAlbum[largeAlbum.length] = 7;
```

### 2) Don't make it any bigger than you need right now

```javascript
let smallAlbum = [3, 8, 1, 12, 5];
```

Oh oh...
But to add to it now, you must create a new array:
```javascript
let newAlbum = new array(smallAlbum.length + 1);
let index;
for ( index = 0; i < smallAlbum.length; index++) {
  newAlbum[index] = smallAlbum[index];
}
newAlbum[index+1] = 7;
```

The point is, hopefully, you've predefined your array big enough for your needs.

___

### Now what if I want to delete a photo from the album... say the picture 12
```javascript
let myAlbum = [3, 8, 1, 12, 5];
let pictureToDelete = 12;
let index;
let indexToDelete;

// first find the picture to delete
for (index = 0 ; index < myAlbum.length ; index++ ) {
  if(myAlbum[index] === pictureToDelete) {
    indexToDelete = index;
    break;
  }
}

// now we can overwrite it, shifting all elements over by one
for (index = indexToDelete; index < myAlbum.length ; index++ ) {
  myAlbum[index] = myAlbum[index+1];
}         
```

Similarly, to add a new picture, say after picture 12, you need to copy all elements from picture 12 onwards over one. So much copying, sigh... what if we had to copy much larger elements... yikes!

This is because the data of an array resides contiguously in memory (side-by-side).
___


## What if we wanted to avoid all of this copying over? ...and avoid this memory restriction?

Let's pair our data with a second property... one that tells us where the next element is. Then they wouldn't need to be side-by-side like in an array... they could reside anywhere in memory! Sweet!

### Let's define our node

```javascript
class Node {
  constructor(value) {
    this.data = value;
    this.next = null;
  }
}
```
### And our linked list

```javascript
class LinkedList {
  constructor(value) {
    this.head = new Node(value);
    this.length = 1;
  }
  
  // functions to edit / manage your linked list
  ...
}
```

## Now what do we need to do to remove picture 12?

Here's the code, but let me draw it out...

```javascript
  remove(valueToDelete) {
    let currentNode = this.head;
    let index = 0;
    let beforeNodeToDelete = null;
    let nodeToDelete = null;

    // the first node is removed
    if (currentNode.data === valueToDelete) {
      this.head = currentNode.next;
      currentNode = null;
      this.length--;
      return;
    }

    beforeNodeToDelete = currentNode;
    // any other node is removed
    while (index <= this.length) {
      if(currentNode.data === valueToDelete) {
        beforeNodeToDelete.next = currentNode.next;
        currentNode = null;
        this.length--;
        break;
      }
      index++;
    }
  }
```

Inserting happens in a similar fashion too.

## Positives of linked lists:
+ Fast insertion / deletion **(no copying of other elements!)**
+ Linked lists let you insert elements at the **beginning of the list** fast ...aka O(1)  ...i.e. same time regardless of size
+ If you keep a **'tail' property** for the last node, like you 'head' property for the first node, inserting at the end of the list is also fast ...O(1).
+ Linked lists also remove the overhead of bothering about the size of the data structure. **The size need not to be known in advance.**

## Drawbacks:
- Slow lookup: need to iterate through the list to find a specific node
- They do use more memory than arrays because of the pointers

### Note
We can also add a **'previous' property** to allow traversal in both directions.
