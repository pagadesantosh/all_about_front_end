### Array.prototype.includes

**Definition**: Determines whether an array includes a certain value among its entries, returning true or false.

```js
//Syntax:
includes(searchElement, fromIndex);
```

<strong>Approach Taken:</strong>

```javascript
if (!Array.prototype.customIncludes) {
  Array.prototype.customIncludes = function (searchElement, fromIndex) {
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    // ex: [1, 2, 3]
    var o = Object(this);

    //ex: 3 is the length of the array in Number format
    var len = Number(o.length) || 0;

    //if array length is 0
    if (len === 0) {
      return false;
    }

    // this pipe is bitwise OR, handles lot of edge scenarios, provided few examples at the bottom
    var n = fromIndex | 0;

    //if index is -100, due to Math.max we will consider it to 0
    var k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);

    // ex: 0 < 3
    while (k < len) {
      if (
        typeof searchElement === 'number' &&
        isNaN(searchElement) &&
        isNaN(o[k])
      ) {
        return true; // Both are NaN
      }
      if (o[k] === searchElement) {
        return true; // Direct comparison
      }
      k++; // Important: Increment the index to avoid an infinite loop
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
```

```js
//bitwise OR examples
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
