## Array.prototype.some:

<strong>Approach Taken:</strong>

```js
if (!Array.prototype.customSome) {
  Array.prototype.customSome = function (callback, thisArg) {
    if (this == null) {
      throw new TypeError(
        'Array.prototype.customSome called on null or undefined'
      );
    }

    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    var array = Object(this); // Ex: ["apple", "banana", "mango", "orange"]
    var len = Math.floor(Math.abs(array?.length)); // to make sure the length is positive and rounded instead of decimals

    for (var i = 0; i < len; i++) {
      // if the mango fruit index(i) is in array, return true
      if (i in array && callback.call(thisArg, array[i], i, array)) {
        return true;
      }
    }

    return false;
  };
}

// Example:
var fruits = ['apple', 'banana', 'mango', 'orange'];

var containsMango = fruits.customSome(function (fruit) {
  return fruit === 'mango';
});

console.log(containsMango); // Should log `true` because "mango" is in the array
```
