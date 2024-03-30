### Array.prototype.includes

**Definition**: Determines whether an array includes a certain value among its entries, returning true or false. If the user provided index is less than or equal to 0, the entire array will be searched(because of while loop runs from 0 to length of array).

```js
//Syntax:
includes(searchElement, fromIndex);
```

```js
// Realtime example usage
const arr = [1,2,3]
console.log(arr.includes(3)) //true
console.log(arr.includes(4)) //false
```

<strong>Approach Taken:</strong>

First two lines are core logics

1. const includesArr = Object(this) is your array
2. includesArr[yourIndex] === searchElement return true
3. Way1: use while loop to iterate using length of array and index (ex: while(index<lengthOfArr))
4. inside while, check if the includes[iterationIndex] === searchElement (if yes return true)
5. outside the while loop, return false (because none of the condition is matched inside while loop)
6. extra conditions to check if array inclues NaN, this can be done with the help of isNaN(searchElement) && isNaN(includesArr[iterationIndex])
7. if index is passed by the user, simply take that into consideration (ex: var index = indexProvided || 0)
8. check if index is in negative condition (ex: const finalIndex = Math.max(index >=0 ? 0 : arrayLength - Math.abs(index), 0))

```javascript
if (!Array.prototype.customIncludes) {
  Array.prototype.customIncludes = function (searchElement, fromIndex) {
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    // ex: [1, 2, 3]
    var inputArr = Object(this);

    //ex: 3 is the length of the array in Number format
    var inputArrLength = Number(inputArr.length) || 0;

    //if array length is 0
    if (inputArrLength === 0) {
      return false;
    }

    // this pipe is bitwise OR, handles lot of edge scenarios, provided few examples at the bottom
    // var newIndex = fromIndex | 0;

    var newIndex = Math.floor(fromIndex) || 0;

    //if index is -100, due to Math.max we will consider it to 0
    var finalIndex = Math.max(
      newIndex >= 0 ? newIndex : inputArrLength - Math.abs(newIndex),
      0
    );

    // ex: 0 < 3
    while (finalIndex < inputArrLength) {
      if (
        typeof searchElement === 'number' &&
        isNaN(searchElement) &&
        isNaN(inputArr[finalIndex])
      ) {
        return true; // Both are NaN
      }
      if (inputArr[finalIndex] === searchElement) {
        return true; // Direct comparison
      }
      finalIndex++; // Important: Increment the index to avoid an infinite loop
    }

    return false;
  };
}

//All examples are passed for the above code:
console.log([1, 2, 3].customIncludes(2)); // true;
console.log([1, 2, 3].customIncludes(4)); // false;
console.log([1, 2, 3].customIncludes(3, 3)); // false;
console.log([1, 2, 3].customIncludes(3, -1)); // true;
console.log([1, 2, NaN].customIncludes(NaN)); // true
console.log(['1', '2', '3'].customIncludes(3)); // false
console.log('----------------------------------------');
const arr = ['a', 'b', 'c'];
console.log(arr.customIncludes('c', 3)); // false
console.log(arr.customIncludes('c', 100)); // false
console.log('----------------------------------------');
console.log(arr.customIncludes('a', -100)); // true
console.log(arr.customIncludes('b', -100)); // true
console.log(arr.customIncludes('c', -100)); // true
console.log(arr.customIncludes('a', -2)); // false
console.log('----------------------------------------');
console.log([1, , 3].customIncludes(undefined)); // true
console.log('----------------------------------------');
const arrayLike = {
  length: 3,
  0: 2,
  1: 3,
  2: 4,
  3: 1, // ignored by includes() since length is 3
};
console.log(Array.prototype.customIncludes.call(arrayLike, 2));
// true
console.log(Array.prototype.customIncludes.call(arrayLike, 1));
// false
```

```js
//bitwise OR examples, it converts nonIntegers, undefined to Integers
4.7 | 0; // Result: 4
```

```js
//ignore semicolon
-3.2 | 0; // Result: -3
```

```js
'hello' | 0; // Result: 0
```

```js
undefined | 0; // Result: 0
```
