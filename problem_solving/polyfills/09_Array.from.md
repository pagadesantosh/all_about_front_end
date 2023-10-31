## Array.from:

#### Convert iterable objects or array-like objects into arrays.

<strong>Approach Taken:</strong>

```js
if (!Array.customFrom) {
  Array.customFrom = function (inputArr, mapFn, thisArg) {
    if (inputArr == null) {
      throw new TypeError('inputArr cannot be null or undefined');
    }

    if (typeof mapFn !== 'undefined' && typeof mapFn !== 'function') {
      throw new TypeError('The map function must be a function');
    }

    // if conditon is true only for the iterables like Strings, Set, Map, Array (More examples are added in the separate code block)
    if (typeof Symbol === 'function' && inputArr[Symbol.iterator]) {
      const arr = [...inputArr]; // this will simply convert into an array ex: Set[ArrayYouProvide] ===> [ArrayYouProvide]
      return mapFn ? arr.map(mapFn, thisArg) : arr; //if mapFn is provided as per the syntax, then map it otherwise as it is.
    }

    // Below rest of the code will only get executed if it is not iterable ex: Objects {}
    const length = Math.floor(Math.abs(inputArr.length));
    const output = Array(length); // if length is 3 then it create 3 empty spaces [null, null, null]

    for (let i = 0; i < length; i++) {
      output[i] = inputArr[i]; // each empty space will be replaced with the inputArr[i]
    }

    return mapFn ? output.map(mapFn, thisArg) : output;
  };
}

// Example Usage:

// #1 An array-like object
const arrayLike = { 0: 'zero', 1: 'one', 2: 'two', length: 3 };

// Converting the array-like object to an array and transforming each element
const array = Array.customFrom(arrayLike, (value) => value.toUpperCase());

console.log(array); // Should log ["ZERO", "ONE", "TWO"]

// #2 Creating a Set
const set = new Set([1, 2, 3, 4, 5]);

// Converting the Set to an array using `Array.customFrom`
const setArray = Array.customFrom(set);

console.log(setArray); // Should log [1, 2, 3, 4, 5]
```

```js
// Example 1: Strings are iterable objects.
const inputArr = 'Hello';
const newArray = Array.customFrom(inputArr);
console.log(newArray); // Logs ["H", "e", "l", "l", "o"]
```

```js
// Example 2: Sets are also iterable
const inputArr = new Set([1, 2, 3, 4, 5]);
const newArray = Array.customFrom(inputArr);
console.log(newArray); // Logs [1, 2, 3, 4, 5]
```

```js
// Example 3: Maps are iterable too
const inputArr = new Map([
  ['one', 1],
  ['two', 2],
]);
const newArray = Array.customFrom(inputArr);
console.log(newArray); // Logs [["one", 1], ["two", 2]]
```

```js
// Example 4: Array like object not a true iterable
// Array-like objects have a length property and indexed elements, but they do not have the [Symbol.iterator] property, which true iterables like arrays, strings, maps, and sets have.
const arrayLike = { 0: 'zero', 1: 'one', 2: 'two', length: 3 };
```
