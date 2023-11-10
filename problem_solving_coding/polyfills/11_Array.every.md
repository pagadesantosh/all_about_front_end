## Array.prototype.every

<strong>Approach Taken:</strong>


```js
if (!Array.prototype.customEvery) {
  Array.prototype.customEvery = function (callback, thisArg) {
    if (this == null) {
      throw new TypeError(
        'Array.prototype.customEvery called on null or undefined'
      );
    }

    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    var array = Object(this); // Ex: ["apple", "banana", "mango", "orange"]
    var len = Math.floor(Math.abs(array?.length)); // to make sure the length is positive and rounded instead of decimals

    for (var i = 0; i < len; i++) {
      // if the mango fruit index(i) is not in array, return false and exit
      if (i in array && !callback.call(thisArg, array[i], i, array)) {
        return false;
      }
    }

    return true;
  };
}

// Example:
var fruits = ['mango', 'mango', 'mango', 'mango'];

var containsMango = fruits.customEvery(function (fruit) {
  return fruit === 'mango';
});

console.log(containsMango); // Should log `true` because "mango" is in the array
```
