# Session 1: Basics

## Programming Paradigms

### Functional

### Object Oriented

### Component Oriented

### Aspect Oriented

### Distributed



### Software Design Principles


## Separation of Concerns

Logical separation between pieces or "layers" of an application.
```(javascript)
class Cart extends Component {

  render() {
    return (
        <p class="total">
          { this.state.subTotal * 1.13 } // add tax to subTotal
        </p>
      )
  }
}

```
In the above example we are calculating tax in a component meant for just rendering some UI.
What are some problems with this?

Two ways:
```(javascript)
render() {
  return (
      <p class="total">
        { this.props.total } // this component should not be responsible at all for calculations
      </p>
    )
}
```
**OR**
```(javascript)
import TaxCalculator from 'tax-calc';

class Cart extends Component {

  render() {
    return (
        <p class="total">
          { this.calculateTotal(this.state.subTotal) }
        </p>
      )
  }

  calculateTotal(subTotal) {
    const ontarioTaxCalculator = TaxCalculator('on');
    const tax = ontarioTaxCalculator.getTax(subTotal);
    return subTotal + tax;
  }
}

```
Another example of Separation of concerns in React would be using Redux to handle state changes and propagation throughout application.

## Single Responsibility

Consider:
```(javascript)
function sortAndReverseString(string) {};
```
This function is challenging to debug & write automated tests for. How do we know if the sorting is failing or the reversing is failing if both are manipulating the string.

What if we only want to sort? Or only reverse?
```(javascript)
function sort(string) {
  return string.split('').sort().join('');
}

function reverse(string) {
  return string.split('').reverse().join('');
}
```
We now have 2 discrete functions that can be individually used, tested or debugged.
The responsibility of each function is clearly defined by the name (or by tests that describe it).


## Composition

Building on the previous example, how can we compose small, well-defined, discrete pieces of functionality to build more complex functionality.

```(javascript)
// Straight forward
const sortedString = sort('fedcba'); // abcdef
const sortedAndReversed = reverse(sortedString); // fedcba

// one-liner
const sortedAndReversed = reverse(sort(myString))
```

Some libraries provide more functionality for composing functions:
```(javascript)
const sortAndReverse = compose(sort, reverse);
sortAndReverse('fedcba') // fedcba
```


## LoD / Encapsulation

Law of Demeter or principle of least knowledge. Components should not know or attempt to modify the inner workings of others (black box).
React example:
```(javascript)

const options = ['one', 'two', 'three'];
const dropdown = <DropdownComponent items={ options } />;

// THIS IS TERRIBLE NEVER DO THIS
dropdown.state.optionList.orderAscending();

```
Logic related to how the dropdown renders itself should be *encapsulated* within the dropdown component.
No one outside should be directly calling methods on properties on this dropdown component.
Any functionality that should be "public" should be exposed through a clear interface with limited "side effects".
i.e.
```(javascript)
dropdown.sortOptions('asc');

```

## DRY

Don't repeat yourself!
But also don't try to optimize prematurely.
When you discover duplicated functionality, think about how it can be encapsulated and shared.
Within your UI: duplicated markup should be separated into it's own component and configured via props.
Within business logic: duplicated code can be separated into it's own module with a public interface to be used by any other module.



## Recursion



## Low Level

### Call Stacks

### Memory

### Threading
