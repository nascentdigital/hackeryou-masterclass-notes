## Data Structures

### List / Array
An array is an ordered collection of data (either primitive or object depending upon the language). Arrays are used to store multiple values in a single variable. This is compared to a variable that can store only one value. 


```ecmascript 6
let employees = [
  {
    id: '2',
    name: 'Clark',
    position: 'CEO'
  }, 
  {
    id: '1',
    name: 'Diana',
    position: 'CTO'
  }, 
  {
    id: '3',
    name: 'Bruce',
    position: 'COO'
  }
]
```

Each item in an array has a number attached to it, called a numeric index, that allows you to access it. In JavaScript, arrays start at index zero and can be manipulated with various methods. 

```ecmascript 6
const ceo = employees[0] // Clark
const cto = employees[1] // Diana
const coo = employees[2] // Bruce
```
This works, but what type of problems can occur?

```ecmascript 6
employees.shift()

employees.splice(2, 0, {
  id: '4',
  name: 'Barry',
  position: 'Manager'
})


console.log(ceo) // Diana
console.log(cto) // Bruce
console.log(coo) // Barry

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

****
### Dictionary
A Dictionary (aka. Map or Hash Table) is a key-value store of a collection of data. Each key is unique and has only one associated value.

Two types*:
```ecmascript 6
// object
const employees = {
  ceo: {
    id: '2',
    name: 'Clark',
    position: 'CEO'
  }, 
  cto: {
    id: '1',
    name: 'Diana',
    position: 'CTO'
  }, 
  coo: {
    id: '3',
    name: 'Bruce',
    position: 'COO'
  }
}
```
 
```ecmascript 6
// map
const employees = new Map()
employees.set('ceo', {
  id: '2',
  name: 'Clark',
  position: 'CEO'
})
employees.set('cto', {
  id: '1',
  name: 'Diana',
  position: 'CTO'
})
employees.set('coo', {
  id: '3',
  name: 'Bruce',
  position: 'COO'
})
```

Compare this with how we were retrieving `ceo` from the list.

Even if we add or remove items from the map, the way to retrieve them remains the same
```ecmascript 6
employees['manager'] = {
 id: '4',
 name: 'Barry',
 position: 'Manager'
}

delete employees.manager

const { 
  ceo, // Clark 
  cto, // Diana
  coo  // Bruce
} = employees

employees.get('ceo') // Clark
employees.get('cto') // Diana
employees.get('coo') // Bruce
```
The key of an `Object` must be a string (or `Symbol`), whereas a `Map` can have a key of any other data type.

#### Set
`Set` objects are collections of values. You can iterate through the elements of a set in insertion order. A value in the Set may only occur once; it is unique in the Set's collection.

```ecmascript 6
const positionSet = new Set()
positionSet.add('ceo')
positionSet.add('cto')
positionSet.add('cfo') // Set(3) {"ceo", "cto", "cfo"}
positionSet.add('ceo') // Set(3) {"ceo", "cto", "cfo"}
positionSet.delete('ceo') // Set(2) {"cto", "cfo"}
```

Note that two objects with the same properties and values are not considered unique, unless it references the same object

**For example:**
```ecmascript 6
const employeeSet = new Set()
employeeSet.add(coo)
const newCOO = {
 id: '3',
 name: 'Bruce',
 position: 'COO'
}
employeeSet.add(newCOO) // Set(2) {{ id: '3', name: 'Bruce', position: 'COO' }, { id: '3', name: 'Bruce', position: 'COO' }}

const chiefOperatingOfficer = coo
employeeSet.add(chiefOperatingOfficer) // Set(2) {{ id: '3', name: 'Bruce', position: 'COO' }, { id: '3', name: 'Bruce', position: 'COO' }}
```

#### What happens when we need to sort?
For objects, since it is a key-value store, there is no way you can sort values. This is one of the main reasons we would use an array over objects in certain situations.

The object has to somehow be converted into a list and sorted from there.

```ecmascript 6
const employeeKeys = Object.keys(employees)
// sort descending by id
const ids = employeeKeys.map(employeeKey => {
  return employees[employeeKey].id
})

ids.sort()
const sortedEmployees = ids.map(id => employees[id])
``` 
***
### Key differences between Lists and Dictionaries and when to use
- Although they are both used to collect data, the way they are used to access items differ
  - Array items are accessed based on index, so** order **matters
  - Dictionary items are accessed based on a *unique* key, so they are **unordered**
- Arrays are better used to list items, whereas Dictionaries are used for lookups   

Sources:
- https://developer.mozilla.org/en-US/docs/Glossary/array
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set
- https://www.tutorialspoint.com/data_structures_algorithms/hash_data_structure.htm
- https://code.tutsplus.com/articles/data-structures-with-javascript-stack-and-queue--cms-23348