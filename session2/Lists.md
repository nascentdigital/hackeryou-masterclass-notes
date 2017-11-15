### Array
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
]
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
employees.shift()

employees.splice(2, 0, {
  id: '4',
  name: 'Barry',
  position: 'Manager'
})

ceo = employees[0] // Clark
cto = employees[1] // Diana
coo = employees[2] // Bruce
```

When we add items or change the *order* of items, we can no longer expect the values to still be at a given index

#### How do we find an employee/employees then?
```ecmascript 6
let ceo;
for (let index = 0; index < employees.length; index++) {
  const employee = employees[index]
  if (employee.position === 'CEO') {
    ceo = employee
    break
  }
}

let managers = []
for (let index = 0; index < employees.length; index++) {
  const employee = employees[index]
  if (employee.position === 'Manager') {
    managers.push(employee)
  }
} 
```

**OR**
```ecmascript 6
const ceo = employees.find(employee => employee.position === 'CEO')

// or

const managers = employees.filter(employee => employee.position === 'Manager')
```

****

### Stack and Queue
- Stacks and queues are used to organize data into sequential order
- A stack is LIFO (Last In First Out)
- A Queue is FIFO (First In First Out)
- Both are abstract data types, and in Javascript are not actual data types, they can both be implemented though

```ecmascript 6
// stack
const stack = []
stack.push(1);
const last = stack.pop()

// queue
const queue = []
queue.push(1)
const first = queue.shift()
``` 
