
# Helpful Libraries
Along with certain ES6 methods for arrays and objects, there are also helpful Javascript libraries out there with performant methods that you can use without digging too much into the implementation of the specific algorithms.
Some good examples are [Underscore](underscorejs.org) and [Lodash](https://lodash.com/).



## Helpful methods in LoDash

Below are some of the more commonly used methods within lodash when working with data.
### Arrays
```
_.indexOf(array, value, [fromIndex=0])
_.sortedIndexOf(array, value)
_.find(collection, [predicate=_.identity], [fromIndex=0])
_.concat(array, [values])
_.uniq(array)
_.intersection([arrays])
```

### Collections
```
_.sortBy(collection, [iteratees=[_.identity]])
_.orderBy(collection, [iteratees=[_.identity]], [orders])
_.find(collection, [predicate=_.identity], [fromIndex=0])
_.filter(collection, [predicate=_.identity])
```

### Objects
```
_.findKey(object, [predicate=_.identity])
_.merge(object, [sources])
_.mergeWith(object, sources, customizer)
```
[LoDash docs](https://lodash.com/docs/)
