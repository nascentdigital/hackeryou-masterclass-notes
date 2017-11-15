### Arrays
An array is an ordered collection of data (either primitive or object depending upon the language). Arrays are used to store multiple values in a single variable. This is compared to a variable that can store only one value. 

```ecmascript 6
const ceo = {
  id: '2',
  name: 'Clark',
  position: 'CEO'
}
const cto = {
  id: '1',
  name: 'Diana',
  position: 'CTO'
}
 const coo = {
  id: '3',
  name: 'Bruce',
  position: 'COO'
}

```

```ecmascript 6
let employees = [
  ceo,
  cto,
  coo
]
```

Each item in an array has a number attached to it, called a numeric index, that allows you to access it. In JavaScript, arrays start at index zero and can be manipulated with various methods. 

```ecmascript 6
let ceo = employees[0] // Clark
let cto = employees[1] // Diana
let coo = employees[2] // Bruce
```
This works, but what type of problems can occur?

```ecmascript 6
// remove an employee from the front of the array
employees.shift()

// add an employee at the 2nd index
employees.splice(2, 0, {
  id: '4',
  name: 'Barry',
  position: 'Manager'
})

// our employees are no longer at the same indexes
ceo = employees[0] // Diana
cto = employees[1] // Bruce
coo = employees[2] // Barry
```

When we add items or change the *order* of items, we can no longer expect the values to still be at a given index

#### How do we find an employee/employees then?
```ecmascript 6
const find = (list, callback) => {
    for (let index = 0; index < list.length; index++) {
      let match = callback(list[index])
      if (match === true) {
        return list[index]
      }
    }
}

// find the ceo from the list of employees
const ceo = find(employees, employee => employee.position === 'CEO')

const filter = (list, callback) => {
    let matches = []
    for (let index = 0; index < list.length; index++) {
      let match = callback(list[index])
      if (match === true) {
        matches.push(list[index])
      }
    }
    return matches
}
// filter manager from list of employees
// this can potentially return more than one employee
const manager = filter(employees, (employee) => employee.position = 'Manager')
```

**OR**

A Javascript Array object already has these methods
```ecmascript 6
const ceo = employees.find(employee => employee.position === 'CEO')

// or

const manager = employees.filter(employee => employee.position === 'Manager')
```

****

### Stacks and Queues
- Stacks and queues are used to organize data into sequential order
- Both are abstract data types, and in Javascript are not actual data types, they can both be implemented though
 
A stack is LIFO (Last In First Out)

Let's say we needed to keep the history of some changes, like in paint program to draw portraits.
```ecmascript 6
// stack
class Paint {
    constructor() {
        this.history = []
    }
    
    draw(shapes) {
        this.history.push(shapes)
    }
    
    undo() {
        this.history.pop()
    }
}

// instantiate our paint program
const paint = new Paint()
// doing things will add to our history of shapes
paint.draw('face') 
paint.draw('eye')
paint.draw('eye')
paint.draw('moustache')
paint.undo() // moustache

paint.draw('nose')
paint.draw('ears')
paint.draw('earrings')
paint.draw('glasses')
paint.undo() // glasses
paint.undo() // earrings

// we now have a beautiful portrait with eyes, a nose, and ears
```

A Queue is FIFO (First In First Out)

Implement a program that sells milk, sort of like a vending machine
```ecmascript 6
class MightyMilkMachine() {
    contructor() {
        this.inventory = []
    }
    
    stock(carton) {
        this.inventory.push(carton)
    }
    
    sell() {
        return this.inventory.shift()
    }
}

// instantiate our machine
const milkMachine = new MightyMilkMachine()
// someone stocks it up
milkMachine.stock({
    expiry: 'Aug 1, 2018',
    flavour: 'plain'
})

milkMachine.stock({
    expiry: 'Aug 5, 2018',
    flavour: 'chocolate'
})

milkMachine.stock({
    expiry: 'Oct 21, 2018',
    flavour: 'strawberry'
})

// now a customer comes and wants some milk
milkMachine.sell() // { expiry: 'Aug 1, 2018', flavour: 'plain' } 
milkMachine.sell() // { expiry: 'Aug 5, 2018', flavour: 'chocolate' } 
```
