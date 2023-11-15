1. **Array.prototype.includes**: Implement the `includes` method for arrays.

```js
//Definition
Determines whether an array includes a certain value among its entries, returning true or false.
```

```js
//Syntax:
includes(searchElement, fromIndex);
```

<details>
<summary>View Answer</summary>

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

</details>

---

2. **Array.prototype.findIndex**: Implement the `findIndex` method for arrays.

```js
//Definition:
The findIndex() method of Array Instances returns the `index of the first element` in an array that satisfies the provided testing function.
If no elements are matched, it returns -1
```

```js
//Syntax:
findIndex(callbackFn, thisArg);
```

<details>
<summary>View Answer</summary>

```js
if (!Array.prototype.customFindIndex) {
  Array.prototype.customFindIndex = function (callback, thisArg) {
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    if (typeof callback !== 'function') {
      throw new TypeError('callback must be a function');
    }

    const o = Object(this);
    const len = Number(o.length) || 0;

    let k = 0;
    while (k < len) {
      //searched element value at particular index ex: arr[0] will be 5
      const kValue = o[k];
      //thisArg, searchElement, index, array
      if (callback.call(thisArg, kValue, k, o)) {
        return k;
      }
      k++;
    }

    return -1;
  };
}

//Example 1
const array1 = [5, 12, 8, 130, 44];
const isLargeNumber = (element) => element > 13;
console.log(array1.customFindIndex(isLargeNumber));
// Expected output: 3, because 130 is at index 3

//Example 2
const numbers = [-3, 8, 9, -5, 7, -2];
const index = numbers.customFindIndex((num) => num < 0);
console.log(index); // Output:  (because -3 is the first negative number and its index is 0)

//Example 3
const people = [
  { name: 'John', age: 15 },
  { name: 'Doe', age: 17 },
  { name: 'Anna', age: 22 },
  { name: 'Mike', age: 19 },
];
const index1 = people.customFindIndex((person) => person.age >= 18);
console.log(index1); // Output: 2 (because Anna is the first adult and her index is 2)

//Example 4
const words = ['apple', 'banana', 'cherry', 'date'];
const index2 = words.customFindIndex((word) => word.length > 5);
console.log(index2); // Output: 1 (because "banana" has a length of 6 and its index is 1)

//Example 5
const library = [
  { title: 'Moby Dick', author: 'Herman Melville' },
  { title: '1984', author: 'George Orwell' },
  { title: 'Brave New World', author: 'Aldous Huxley' },
];
const index3 = library.customFindIndex((book) => book.title === '1984');
console.log(index3); // Output: 1
```

</details>

---

3. **Array.isArray**: Implement a function to check if a given input is an array.

```js
//Definition:
Determines whether the passed value is an Array
```

```js
//Syntax:
Array.isArray(value);
```

<details>
<summary>View Answer</summary>

One common approach is to use the `Object.prototype.toString.call()` method to get the object type as a string and check if it is "[object Array]". Here is an example implementation:

```javascript
//customArray function is the correct way
Array.customArray = function (input) {
  return Object.prototype.toString.call(input) === '[object Array]';
};

console.log('Array.isArray([])', Array.isArray([])); //true
console.log('Array.isArray({})', Array.isArray({})); //false
console.log('Array.customArray([])', Array.customArray([])); //true
console.log('Array.customArray({})', Array.customArray({})); //false
```

```js
//if you want to achieve prototype fashion then below is the way
Array.prototype.customArray = function () {
  return Object.prototype.toString.call(this) === '[object Array]';
};

const arr = [];
console.log('arr.customArray', arr.customArray()); //true
const obj = {};
console.log('obj.customArray', obj.customArray); // undefined
```

</details>

---

4. **Object.create**:

```js
//Definition:
Is used to create a new object using an existing object as the prototype of the newly created object.
```

```js
//Object.create(proto, propertiesObject)
```

<details>
<summary>View Answer</summary>

```js
function createObject(proto) {
  if (proto === null || typeof proto !== 'object') {
    throw new Error('Argument must be the object, or null');
  }

//empty function
  function F() {}
  //prototype chaining with proto as the value
  F.prototype = proto;
  //return the new Function
  return new F();
}

const person = {
  key: 'value',
  sayHello() {
    console.log('Hello!');
  },
};

const john = createObject(person);
john.sayHello(); // Hello
console.log('person object', person); // person object {key: 'value', sayHello: ƒ}
console.log('john object', john); // john object F {}
console.log('john object', john.key); // john object value
// it does create an new object with prototype property
const newObj = Object.create(person);
console.log('newObj object', newObj); // newObj object {}
console.log('Are they equal', newObj === john); // false
console.log('Are they equal', person === john); // false
console.log('Are they equal', john === john); // true
```

</details>

---

5. **String.prototype.startsWith**: Implement the `startsWith` method for strings.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- String prototype is equal to a function that accepts two arguments, first one is what you want to search and second arg is from which position you want to start ex: 0 or 1 or 10...
- if no position is passed, consider it as 0, else consider whatever is passed (ex: ternay operator)
- this keyword points to the complete string and we can do .substring to this with pos, pos+ search.length and do triple equal check with the passed argument

ex: "Hello world".substring(0, 5) === "Hello" which returns true

```js
if (typeof String.prototype.customStartsWith !== 'function') {
  String.prototype.customStartsWith = function (search, rawPos) {
    var pos = rawPos > 0 ? rawPos : 0;
    // this.substring(pos, pos + search.length) is nothing but
    // "Complete string passed in the left".substring(pos, 1+pos) ex: "Hello" if no pos is passed === "String you passed in right" ex: "Hello"
    return this.substring(pos, pos + search.length) === search;
  };
}

// Example Usage
console.log('Hello world'.customStartsWith('Hello', 1)); // expected output: false
console.log('Hello world'.customStartsWith('world')); // expected output: false
```

</details>

---

6. **String.prototype.endsWith**: Implement the `endsWith` method for strings.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- if no position is provided then we are considering length as the entire string length ex: 11 for "Hello world" and using this length for substring calculation.
- this.substring(entire string length - search.length, entire string length)
  ex: "Hello world".substring(6, 11) === "world"

```js
if (!String.prototype.customEndsWith) {
  String.prototype.customEndsWith = function (search, this_len) {
    if (this_len === undefined || this_len > this.length) {
      // if no position is provided then consider it as Entire string length ex: 11 for Hello world
      this_len = this.length;
    }
    // "Hello world".substring(6, 11) === "world"
    return this.substring(this_len - search.length, this_len) === search;
  };
}

// Example Usage
console.log('Hello world'.customEndsWith('world')); // expected output: true
console.log('Hello world'.customEndsWith('Hello')); // expected output: false
```

</details>

---

7. **String.prototype.repeat**: Implement the `repeat` method for strings.

<details>
<summary>View Answer</summary>

```js
String.prototype.customRepeat = function (count) {
  if (typeof count !== 'number' || count < 0 || count === Infinity) {
    throw new RangeError('Invalid count value');
  }

  // we always want count to be in integers ex: 1.3 to 1
  count = Math.floor(count);

  let result = '';
  // pattern is nothing but at first it prints whatever you want to repeat (ex: 'Hello ')
  let pattern = this.valueOf();

  // runs this while loop until count is 0
  while (count > 0) {
    // checking for odd numbers
    if (count % 2 === 1) {
      result = result + pattern;
    }

    count = Math.floor(count / 2);

    if (count > 0) {
      pattern = pattern + pattern;
    }
  }

  return result;
};

// Example Usage
console.log('Hello '.customRepeat(2)); // "Hello Hello "
```

</details>

---

8. **Promise**: Implement a basic promise with `resolve`, `reject`, `then`, and `catch`.

<details>
<summary>View Answer:</summary>

```javascript
function MyPromise(executor) {
  var state = 'pending';
  var value = undefined;
  var reason = undefined;
  var onResolvedCallbacks = [];
  var onRejectedCallbacks = [];

  function resolve(val) {
    if (state === 'pending') {
      state = 'fulfilled';
      value = val;
      for (var i = 0; i < onResolvedCallbacks.length; i++) {
        onResolvedCallbacks[i](value);
      }
    }
  }

  function reject(res) {
    if (state === 'pending') {
      state = 'rejected';
      reason = res;
      for (var i = 0; i < onRejectedCallbacks.length; i++) {
        onRejectedCallbacks[i](reason);
      }
    }
  }

  try {
    executor(resolve, reject);
  } catch (e) {
    reject(e);
  }

  this.then = function (onFulfilled, onRejected) {
    if (state === 'fulfilled' && typeof onFulfilled === 'function') {
      onFulfilled(value);
    } else if (state === 'rejected' && typeof onRejected === 'function') {
      onRejected(reason);
    } else if (state === 'pending') {
      if (typeof onFulfilled === 'function') {
        onResolvedCallbacks.push(onFulfilled);
      }
      if (typeof onRejected === 'function') {
        onRejectedCallbacks.push(onRejected);
      }
    }
  };

  this.catch = function (onRejected) {
    this.then(null, onRejected);
  };
}

// Example usage
var promise = new MyPromise(function (resolve, reject) {
  setTimeout(function () {
    resolve('Success!');
  }, 1000);
});

promise
  .then(function (value) {
    console.log(value);
  })
  .catch(function (error) {
    console.error(error);
  });
```

</details>

---

9. **Array.from**: Convert iterable objects or array-like objects into arrays.

<details>
<summary>View Answer</summary>

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

</details>

---

10. **Array.prototype.some**: Implement the `some` method for arrays.

<details>
<summary>View Answer</summary>

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

</details>

---

11. **Array.prototype.every**: Implement the `every` method for arrays.

<details>
<summary>View Answer</summary>

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

</details>

---

12. **Number.isNaN**: Implement a function to determine if the passed value is NaN.

<details>
<summary>View Answer</summary>

```js
// Good thing about Number.isNaN() doesn't attempt to convert the parameter to a number, so non-numbers always return false.

if (!Number.isCustomNaN) {
  Number.isCustomNaN = function (value) {
    return value !== value;
  };
}
```

```js
console.log(Number.isNaN(NaN)); // expected output: true
console.log(Number.isNaN(undefined)); // expected output: false
console.log(Number.isNaN(37)); // expected output: false
```

```js
// All of them are non-numbers and returns false for every operation

Number.isNaN('NaN'); //false
Number.isNaN(undefined); //false
Number.isNaN({}); //false
Number.isNaN('blabla'); //false
Number.isNaN(true); //false
Number.isNaN(null); //false
Number.isNaN('37'); //false
Number.isNaN('37.37'); //false
Number.isNaN(''); //false
Number.isNaN(' '); //false
```

```js
// All of them returns true
console.log(Number.isNaN(NaN)); // expected output: true
console.log(Number.isNaN(undefined / 5)); // expected output: true
console.log(Number.isNaN('text' / 2)); // expected output: true
console.log(Number.isNaN(Math.sqrt(-1))); // expected output: true
console.log(Number.isNaN(Number.NaN)); // expected output: true
```

</details>

---

13. **Number.isInteger**: Implement a function to determine if the passed value is an integer.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. Check typeOf value is number, isFinite(value) is true and compare it is the same value you passed after round off ex: Math.floor(value) === value

```js
if (!Number.isCustomInteger) {
  Number.isCustomInteger = function (value) {
    return (
      typeof value === 'number' &&
      isFinite(value) &&
      Math.floor(value) === value
    );
  };
}
```

```js
console.log(Number.isCustomInteger(0)); // expected output: true
console.log(Number.isCustomInteger(1)); // expected output: true
console.log(Number.isCustomInteger(-100000)); // expected output: true
console.log(Number.isCustomInteger(9999999999)); // expected output: true
console.log(Number.isCustomInteger(0.1)); // expected output: false
console.log(Number.isCustomInteger(Math.PI)); // expected output: false
console.log(Number.isCustomInteger(NaN)); // expected output: false
console.log(Number.isCustomInteger(Infinity)); // expected output: false
console.log(Number.isCustomInteger(-Infinity)); // expected output: false
console.log(Number.isCustomInteger('10')); // expected output: false
console.log(Number.isCustomInteger(true)); // expected output: false
console.log(Number.isCustomInteger(false)); // expected output: false
console.log(Number.isCustomInteger([1])); // expected output: false
```

</details>

---

14. **Object.keys**: Implement a method to return an array of a given object's own enumerable property names.

<details>
<summary>View Answer</summary>

```js
if (!Object.customKeys) {
  Object.customKeys = function (obj) {
    if (obj == null || (typeof obj !== 'object' && typeof obj !== 'function')) {
      throw new TypeError('Object.customKeys called on non-object');
    }

    var keys = [];
    for (var prop in obj) {
      if (Object.prototype.hasOwnProperty.call(obj, prop)) {
        keys.push(prop);
      }
    }
    return keys;
  };
}

var obj = {
  a: 1,
  b: 2,
  c: 3,
  d: 'apple',
};

var keys = Object.customKeys(obj);
console.log(keys); // expected output: ['a', 'b', 'c']
```

</details>

---

15. **Object.values**: Implement a method to return an array of a given object's own enumerable property values.

<details>
<summary>View Answer</summary>

```js
if (!Object.customValues) {
  Object.customValues = function (obj) {
    if (obj == null || (typeof obj !== 'object' && typeof obj !== 'function')) {
      throw new TypeError('Object.customValues called on non-object');
    }

    var values = [];
    for (var prop in obj) {
      if (Object.prototype.hasOwnProperty.call(obj, prop)) {
        values.push(obj[prop]);
      }
    }
    return values;
  };
}

var obj = {
  a: 1,
  b: 2,
  c: 3,
};

var customValues = Object.customValues(obj);
console.log(customValues); // expected output: [1, 2, 3]
```

</details>

---

16. **Object.entries**: Implement a method to return an array of a given object's own enumerable property `[key, value]` pairs.

<details>
<summary>View Answer</summary>

```js
if (!Object.customEntries) {
  Object.customEntries = function (obj) {
    if (obj == null || (typeof obj !== 'object' && typeof obj !== 'function')) {
      throw new TypeError('Object.customEntries called on non-object');
    }

    var entries = [];
    for (var prop in obj) {
      if (Object.prototype.hasOwnProperty.call(obj, prop)) {
        entries.push([prop, obj[prop]]);
      }
    }
    return entries;
  };
}

var obj = {
  a: 1,
  b: 2,
  c: 3,
};

var customEntries = Object.customEntries(obj);
console.log(customEntries); // expected output: [["a", 1], ["b", 2], ["c", 3]]
```

</details>

---

**17. Implement Promise.any polyfill**

<details>
<summary>View Answer</summary>

```js
if (typeof Promise.any !== 'function') {
  Promise.customAny = function (promises) {
    return new Promise((resolve, reject) => {
      if (!Array.isArray(promises)) {
        return reject(new TypeError('it will only accept arrays'));
      }
      if (promises.length === 0) {
        return reject(new TypeError('The array of promises cannot be empty'));
      }

      let errors = [];
      promises.forEach((promise) => {
        // The reason to use Promise.resolve(promise) is to ensure that the following .then and .catch methods can be consistently used, whether we are dealing with a promise or a plain value.
        // When a rejected promise is passed to Promise.resolve, it returns the same rejected promise.
        // It does not change a rejected promise into a resolved one or alter the promise in any way.
        // The .then method is skipped for rejected promises, and the .catch method is invoked instead.
        Promise.resolve(promise)
          .then((value) => resolve(value))
          .catch((error) => {
            errors.push(error);
            if (errors.length === promises.length) {
              return reject(
                new AggregateError(
                  errors,
                  'all the promises passed are of rejected'
                )
              );
            }
          });
      });
    });
  };
}

// Usage example
const p1 = Promise.reject('Failed 1');
const p2 = Promise.resolve('Succeed 2');
const p3 = Promise.reject('Failed 3');

Promise.customAny([p1, p2, p3])
  .then((value) => console.log(value)) // Logs: 'Succeed 2'
  .catch((error) => console.error(error));

// Example 2
const promise1 = Promise.reject('Failed 1');
const promise2 = 'Succeeded'; // This is a plain value, not a promise
const promise3 = Promise.reject('Failed 3');

Promise.customAny([promise1, promise2, promise3])
  .then((value) => console.log(value)) // Logs: 'Succeeded'
  .catch((error) => console.error(error));

//Example 3
const rejectedPromise = Promise.reject('Failed');

// This will not change the state of the rejected promise
const stillRejectedPromise = Promise.resolve(rejectedPromise);

stillRejectedPromise
  .then(() => console.log('This will not be logged'))
  .catch((error) => console.log(error)); // This will log: 'Failed'

// Rejected promises remain rejected and invoke the .catch handler, while resolved promises or plain values invoke the .then handler.
```

</details>

---

**18. Implement Promise.all polyfill**

```js
if (typeof Promise.all !== 'function') {
  Promise.all = function (promises) {
    return new Promise((resolve, reject) => {
      if (!Array.isArray(promises)) {
        return reject(new TypeError('The input should be an array'));
      }

      let resolvedCount = 0;
      const results = new Array(promises.length);

      if (promises.length === 0) {
        // if the condition is true, it means there are no promises to process,
        // so the Promise.all promise is resolved immediately with an empty results array, and the function returns early.
        return resolve(results);
      }

      promises.forEach((promise, index) => {
        Promise.resolve(promise)
          .then((value) => {
            resolvedCount++;
            results[index] = value;

            if (resolvedCount === promises.length) {
              resolve(results);
            }
          })
          .catch((error) => {
            reject(error);
          });
      });
    });
  };
}

// Usage example
const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3])
  .then((values) => console.log(values)) // Logs: [1, 2, 3]
  .catch((error) => console.error(error));

//Example 2, empty array of promises
const urls = []; // In this case, the URLs array is empty
Promise.all(urls.map((url) => fetch(url)))
  .then((results) => console.log(results)) // Logs an empty array []
  .catch((error) => console.error(error));
```

---

**19. Implement cloneDeep polyfill**

```js
function cloneDeep(value) {
  if (typeof value !== 'object' || value === null) {
    // Return primitive types, functions, or null directly
    return value;
  }

  if (Array.isArray(value)) {
    //This conditon is satisfied only when the values are of array for ex: cloneDeep has the hobbies value, then that would satisfies this if conditon
    // Clone arrays
    const arrCopy = [];
    for (let i = 0; i < value.length; i++) {
      arrCopy[i] = cloneDeep(value[i]);
    }
    return arrCopy;
  }

  if (typeof value === 'object') {
    // Clone objects
    const objCopy = {};
    for (const key in value) {
      if (value.hasOwnProperty(key)) {
        objCopy[key] = cloneDeep(value[key]);
      }
    }
    return objCopy;
  }
}

// Usage example
const original = {
  name: 'Alice',
  age: 30,
  address: {
    street: '123 Main St',
    city: 'Nowhere',
  },
  hobbies: ['reading', 'coding'],
};

const copy = cloneDeep(original);

console.log(copy); // Outputs cloned object
console.log(copy !== original); // Outputs: true
console.log(copy.address !== original.address); // Outputs: true
console.log(copy.hobbies !== original.hobbies); // Outputs: true
```

---

**20. Implement groupBy polyfill**

```js
Object.customGroupBy = function (array, callback) {
  if (!Array.isArray(array)) {
    throw new TypeError('First argument must be an array')
  }

  const groups = {}

  array.forEach((item) => {
    //this is the result of (product)=>product.category ex: in simpler terms it is the specific category here (Fruit or Vegetable)
    const group = callback(item)
    if (!groups[group]) {
      // if the groups object doesn't have that group (ex: Fruit as key) then it should create {Fruit: []}
      groups[group] = []
    }
    groups[group].push(item) //{Fruit: []}.push(item) will be {Fruit: [ { name: 'Apple', category: 'Fruit' }]} for the first iteration
  })

  return groups //is an object which has keys like Fruit, Vegetable
}

// Test the Object.customGroupBy function
const products = [
  { name: 'Apple', category: 'Fruit' },
  { name: 'Banana', category: 'Fruit' },
  { name: 'Carrot', category: 'Vegetable' },
  { name: 'Spinach', category: 'Vegetable' },
]

const groupedByCategory = Object.customGroupBy(
  products,
  (product) => product.category
)

console.log(groupedByCategory)

//Output:
{
    "Fruit": [
        {
            "name": "Apple",
            "category": "Fruit"
        },
        {
            "name": "Banana",
            "category": "Fruit"
        }
    ],
    "Vegetable": [
        {
            "name": "Carrot",
            "category": "Vegetable"
        },
        {
            "name": "Spinach",
            "category": "Vegetable"
        }
    ]
}
```

---

**21. Implement JSON.stringify polyfill**

```js
function stringify(data) {
  if (typeof data === 'bigint') {
    throw new Error('Do not know how to serialize a BigInt at JSON.stringify');
  }
  if (typeof data === 'string') {
    return `"${data}"`;
  }
  if (typeof data === 'function') {
    return undefined;
  }
  if (data !== data) {
    return 'null';
  }
  if (data === Infinity) {
    return 'null';
  }
  if (data === -Infinity) {
    return 'null';
  }
  if (typeof data === 'number') {
    return `${data}`;
  }
  if (typeof data === 'boolean') {
    return `${data}`;
  }
  if (data === null) {
    return 'null';
  }
  if (data === undefined) {
    return 'null';
  }
  if (typeof data === 'symbol') {
    return 'null';
  }
  if (data instanceof Date) {
    return `"${data.toISOString()}"`;
  }
  if (Array.isArray(data)) {
    const arr = data.map((el) => stringify(el));
    return `[${arr.join(',')}]`;
  }
  if (typeof data === 'object') {
    const arr = Object.entries(data).reduce((acc, [key, value]) => {
      if (value === undefined) {
        return acc;
      }
      acc.push(`"${key}":${stringify(value)}`);
      return acc;
    }, []);
    return `{${arr.join(',')}}`;
  }
}

//Example1
const person = {
  name: 'Alice',
  age: 25,
  city: 'New York',
};

const jsonString1 = jsonStringify(person);
console.log(jsonString1);
// Expected output: '{"name":"Alice","age":25,"city":"New York"}'

//Example2
const students = [
  { name: 'Bob', grade: 8 },
  { name: 'Charlie', grade: 9 },
  { name: 'David', grade: 10 },
];

const jsonString2 = JSON.stringify(students);
console.log(jsonString2);
// Expected output: '[{"name":"Bob","grade":8},{"name":"Charlie","grade":9},{"name":"David","grade":10}]'

//Example3
const school = {
  name: 'Green Valley High School',
  location: 'California',
  students: [
    { name: 'Eve', grade: 11 },
    { name: 'Frank', grade: 12 },
  ],
  principal: {
    name: 'Mr. Smith',
    age: 50,
  },
};

const jsonString3 = JSON.stringify(school);
console.log(jsonString3);
// The output should be a JSON string representation of the 'school' object
```

---

**22. Implement Array indexOf method?**

```js
Array.prototype.myIndexOf = function (searchElement, fromIndex = 0) {
  //this means array here
  if (this == null) {
    throw new TypeError('"this" is null or not defined');
  }
  const length = Math.max(0, this.length); // Ex: array.length

  //extra check to validate if the array is empty
  if (length === 0) {
    return -1;
  }

  //if 2nd arg is provided then fromIndex will be considered as index otherwise 0 is the index everytime
  let index = fromIndex | 0;

  //if the index you want to search is more than the length of the array then return -1
  if (index >= length) {
    return -1;
  }

  // if the second arg is negative then we are subtracting array length - (Math.abs(index), 0) Ex: 3 - Math.abs(-1), 0 which results 2
  index = Math.max(index >= 0 ? index : length - Math.abs(index), 0);

  while (index < length) {
    // this is the array and we are searching for index
    if (this[index] === searchElement) {
      return index; //finally it returns index
    }
    index++;
  }
  // return -1 if the searchElement is not found as part of the array provided
  return -1;
};

// Test cases
const array = [2, 9, 9];
console.log(array.myIndexOf(2)); // Expected output: 0
console.log(array.myIndexOf(7)); // Expected output: -1
console.log(array.myIndexOf(9, 2)); // Expected output: 2
console.log(array.myIndexOf(2, -1)); // Expected output: -1
console.log(array.myIndexOf(2, -3)); // Expected output: 0
```

---

**23. Implement Array push method?**

```js
Array.prototype.myPush = function (...elements) {
  //checking array is null
  if (this == null) {
    throw new TypeError('this is null or not defined');
  }

  let length = Math.max(0, this.length);
  const addLength = elements.length;

  //if the length you want to add + the length you already have in the array is more than SAFE
  if (length + addLength > Number.MAX_SAFE_INTEGER) {
    throw new TypeError('The number of array is over the MAX_SAFE_INTEGER');
  }

  //basic for loop
  for (let i = 0; i < addLength; i++) {
    // this[length++] = elements[i]
    this[length] = elements[i];
    length += 1;
  }

  //updating array length with the new length
  this.length = length;

  return length; //push returns the length at the end
};

// Test cases
const fruits = ['apple', 'banana', 'mango'];
const newLength = fruits.myPush('pineapple', 'grape');
console.log(newLength); // Expected output: 5
console.log(fruits); // Expected output: ["apple", "banana", "mango", "pineapple", "grape"]

// The following line
this[length++] = elements[i];

// Is equivalent to
this[3] = 'pineapple'; // Add 'pineapple' to the 3rd index of the array
length = 4; // Now increment the length for the next iteration
```

---

**24. Implement Array unshift method?**

```js
Array.prototype.myUnshift = function (...elements) {
  //checking array is null
  if (this == null) {
    throw new TypeError('this is null or not defined');
  }

  //length specifies to the existing array
  let length = Math.max(0, this.length);

  // addLength specifies that how many you are going to add at the start of the array (ex: 2)
  const addLength = elements.length;

  if (addLength === 0) {
    return length;
  }

  // Move the existing array elements to right and leave empty spaces at the start
  for (let i = length - 1; i >= 0; i--) {
    this[i + addLength] = this[i];
  }

  // [undefined, undefined, 'apple', 'banana', 'mango'] will be the result of the this

  //basic for loop based on the new addition data
  for (let i = 0; i < addLength; i++) {
    //elements specify to the data that user want to newly add at the start (ex: 'pineapple')
    this[i] = elements[i];
  }

  const newLength = length + addLength;
  //updating array length with the new length
  this.length = newLength;

  return newLength; //push returns the length at the end
};

// Test cases
const fruits = ['apple', 'banana', 'mango'];
const newLength = fruits.myUnshift('pineapple', 'grape');
console.log(newLength); // Expected output: 5
console.log(fruits); // Expected output: ["apple", "banana", "mango", "pineapple", "grape"]
```

---

**25. Implement Array pop method?**

```js
if (!Array.prototype.customPop) {
  Array.prototype.customPop = function () {
    // Handle the case where the array is empty
    if (this.length === 0) {
      return undefined;
    }

    // Get the last element of the array
    const removedElement = this[this.length - 1];

    // Decrease the array length by 1, thereby removing the last element
    this.length = this.length - 1;

    // Return the removed element
    return removedElement;
  };
}

// Test
const numbers = [1, 2, 3, 4, 5];
const poppedValue = numbers.customPop();
console.log(poppedValue); // Outputs: 5
console.log(numbers); // Outputs: [1, 2, 3, 4]
```

---

**26. Implement Promise.race polyfill**

```js
if (typeof Promise.customRace !== 'function') {
  Promise.customRace = function (promises) {
    return new Promise((resolve, reject) => {
      // Ensure the input is iterable
      if (!Array.isArray(promises)) {
        throw new TypeError(
          'The arguments to Promise.customRace must be an iterable'
        );
      }

      // Resolve or reject the main promise as soon as one of the input promises settles
      for (let p of promises) {
        Promise.resolve(p).then(resolve, reject);
      }
    });
  };
}

// Example Usage
function processLocally(data) {
  return new Promise((resolve) => {
    // Simulated delay for local processing
    setTimeout(() => resolve(`Local result for ${data} 1000ms`), 1000);
  });
}

function processRemotely(data) {
  return new Promise((resolve) => {
    // Simulated delay for remote processing
    setTimeout(() => resolve(`Remote result for ${data} 500ms`), 500);
  });
}

const data = 'sampleTask';
Promise.customRace([processLocally(data), processRemotely(data)])
  .then((result) => console.log(result)) // Outputs: "Remote result for sampleTask 500ms"
  .catch((error) => console.error(error));
```

---

**27. Implement String.split() polyfill**

```js
if (!String.prototype.customSplit) {
  String.prototype.customSplit = function (separator, limit) {
    // Edge case: if separator is not provided or empty, return the whole string in an array
    if (separator === undefined || separator === '') {
      return [this.toString()];
    }

    const result = [];
    let startIndex = 0;

    //separatorIndex logs the index of first comma/separator in the string, ex: for 'Hello,World' it will log as 5
    let separatorIndex = this.indexOf(separator);

    // While the separator is found in the string
    while (separatorIndex !== -1) {
      // If a limit is set and we reached it, break
      if (limit !== undefined && result.length === limit) {
        break;
      }

      //result is an array and we are pushing the first splitted string into this array, ex: ['Hello']
      result.push(this.substring(startIndex, separatorIndex));

      //we are updating startIndex from 0(default) to the (separatorIndex) + (separator.length i.e; (',').length)
      startIndex = separatorIndex + separator.length;

      //updating separatorIndex with newStartIndex ex: logs 11 (reason is second comma after first split)
      separatorIndex = this.indexOf(separator, startIndex);
    }

    // If a limit is set and we reached it, return the result
    if (limit === undefined || result.length < limit) {
      result.push(this.substring(startIndex));
    }

    return result;
  };
}

// Test
const testString = 'Hello,World,This,Is,Test';
console.log(testString.customSplit(',', 2)); // ["Hello", "World", "This", "Is", "Test"]
console.log(testString.customSplit(',')); // ["Hello", "World", "This", "Is", "Test"]
```

---

**28. Implement a custom function similar to `SetTimeout` without using native `setTimeout` or `setInterval` functions** using Web workers or requestAnimationFrame

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- requestAnimationFrame accepts the function as a param
- the passed function in the requestAnimationFrame will get its own timestamp which we use this with performance.now (startTime) with the delay passed while invocation (ex: timestamp - startTime >= delay)
- in the else condition we will be doing the same thing by invoking the requestAnimationFrame(func)
- if condition simply executes the callback
- for better understanding breakdown the code from the output point of view or invocation point of view ex: how do you call the function

```js
function customSetTimeout(callback, delay) {
  const startTime = performance.now();
  console.log('startTime', (startTime / 1000).toFixed(2), 's');
  function checkTime(timestamp) {
    if (timestamp - startTime >= delay) {
      const currentTime = performance.now();
      console.log('currentTime', (currentTime / 1000).toFixed(2), 's');
      const difference = currentTime - startTime;
      console.log('diff', (difference / 1000).toFixed(2), 's');
      callback();
    } else {
      requestAnimationFrame(checkTime);
    }
  }
  requestAnimationFrame(checkTime);
}

customSetTimeout(() => {
  console.log('Executed after delay');
}, 4000);
```

</details>

---

**29. Implement setInterval polyfill**

```js
let rafIntervals = {};

function customSetInterval(callback, delay) {
  const start = performance.now();
  const id = Symbol('rafInterval');

  function loop(timestamp) {
    if (timestamp - start >= delay * (rafIntervals[id].counter + 1)) {
      callback();
      rafIntervals[id].counter++;
    }
    if (!rafIntervals[id].stopped) {
      requestAnimationFrame(loop);
    }
  }

  rafIntervals[id] = {
    counter: 0,
    stopped: false,
  };

  requestAnimationFrame(loop);
  return id;
}

function customClearInterval(id) {
  if (rafIntervals[id]) {
    rafIntervals[id].stopped = true;
    delete rafIntervals[id];
  }
}

// Example usage:
const intervalId = customSetInterval(() => {
  console.log('This runs every 1000ms');
}, 1000);

// To stop the interval after 5 seconds:
setTimeout(() => {
  customClearInterval(intervalId);
  console.log('Interval stopped');
}, 5000);
```

---

**30.Write a polyfill for `Array.reduce()` - Understand accumulator and current value.**

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. For each element of the array, it calls the callback function with the current value of the accumulator, the current element of the array, the current index, and the array itself. It then updates the accumulator with the result of the callback

2. if an initialValue was provided, it sets the accumulator to the initialValue and starts iterating over the array from the beginning.

3. If no initialValue is provided, it checks if the array is empty. If it's empty, it throws a TypeError because you can't reduce an empty array without an initial value. Otherwise, it sets the accumulator to the first element of the array and starts iterating from the second element.

```js
if (!Array.prototype.myReduce) {
  Array.prototype.myReduce = function (callback, initialValue) {
    const arr = arguments[0];

    if (arr === null || arr === undefined) {
      throw new TypeError(
        'Array.prototype.myReduce called on null or undefined'
      );
    }
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    let len = arr.length;
    let accumulator;

    const iterateOverArray = (start) => {
      for (let i = start; i < len; i++) {
        accumulator = callback(accumulator, arr[i], i, arr);
      }
    };

    if (initialValue !== undefined) {
      accumulator = initialValue;
      iterateOverArray(0);
    } else {
      if (len === 0) {
        throw new TypeError('Reduce of empty array with no initial value');
      }
      accumulator = arr[0];
      iterateOverArray(1);
    }

    return accumulator;
  };
}

// Test
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;
console.log(array1.myReduce(reducer)); // Expected output: 10
console.log(array1.myReduce(reducer, 5)); // Expected output: 15
```

</details>

---

**31. Write a polyfill for `Object.assign()`**

<details>
<summary>View Answer</summary>
<strong>Approach Taken:</strong>

- customAssign function takes two arguments, one is target and the object that user declares
- while passing as params we would do some manipulating like we use spread operator for user provided object so that we can use for looping
- just convert your target which is {} into Object(target) ex: target = Object(target)
- sources.forEach and you will get the each and every object and do the Object.keys(passSourceObject) which is nothing but an array so do another forEach and you can access the key of it and save your target[key] with already provided source[key]

```js
if (typeof Object.customAssign !== 'function') {
  Object.customAssign = function (target, ...sources) {
    // sources will be part of the array and can used for looping ex: [{a:1}]
    if (target === null || target === undefined) {
      throw new TypeError('Cannot convert undefined or null to object');
    }

    // converting any non-object if provided to object at the end (so target has to be Object at the end)
    target = Object(target);

    sources.forEach((source) => {
      // source is an object ex: {a:1}
      if (source !== null && source !== undefined) {
        Object.keys(source).forEach((key) => {
          // It checks if the source object has its own property (not inherited) with the given key, and if so, it assigns that property and value to the target object.
          if (Object.prototype.hasOwnProperty.call(source, key)) {
            // whatever is already provided as part of args will be stored in the target object ex: target[key]
            target[key] = source[key];
          }
        });
      }
    });

    return target;
  };
}

// Example usage
const obj1 = { a: 1 };
const copyObj1 = Object.customAssign({}, obj1);
copyObj1.a = 2;

console.log('copyObj1', copyObj1); //copyObj1 {a: 2}
console.log('obj1', obj1); // obj1 {a:1}
```

</details>

---

**32. Write a polyfill for `Array.forEach()`**

<details>
<summary>View Answer</summary>

```js
Array.prototype.customForEach = function (callback, thisArg) {
  const array = this;

  if (array == null) {
    throw new TypeError(
      'Array.prototype.customForEach called on null or undefined'
    );
  }

  if (typeof callback !== 'function') {
    throw new TypeError(callback + ' is not a function');
  }

  for (let i = 0; i < array.length; i++) {
    if (i in array) {
      //calls the callback function with the element value, index, and the array itself as arguments. The thisArg parameter is used as the `this` value inside the callback if provided.
      callback.call(thisArg, array[i], i, array);
    }
  }
};

// Example usage
const arr = [1, 2, 3, 4, 5];
arr.customForEach((item) => {
  console.log(item);
});
```

</details>

---

**33. Write a custom `Array.find()` polyfill**

<details>
<summary>View Answer</summary>
- Loop through array, and return the first item that satisfies the provided testing function.

```js
if (!Array.prototype.customFind) {
  Array.prototype.customFind = function (callback, thisArg) {
    if (this == null) {
      throw new TypeError(
        'Array.prototype.customFind called on null or undefined'
      );
    }

    if (typeof callback !== 'function') {
      throw new TypeError('callback must be a function');
    }

    // is used to convert the this value into an object.
    const array = Object(this);
    const length = array.length >>> 0;

    for (let i = 0; i < length; i++) {
      if (i in array) {
        const element = array[i];
        if (callback.call(thisArg, element, i, array)) {
          //This if statement checks if the callback function returns a truthy value for the current element. If it does, it means that the current element satisfies the testing function, and it should be returned as the found element.
          return element;
        }
      }
    }

    return undefined;
  };
}

// Example usage:
const array = [5, 12, 8, 130, 44];
const found = array.customFind((element) => element > 120);
console.log(found); // Output: 130
```

</details>

---

**34. Write a polyfill for `Function.prototype.bind`**

- Return a bound function with preset context and arguments.

<details>
<summary>View Answer</summary>

```js
if (!Function.prototype.customBind) {
  Function.prototype.customBind = function (context, ...args) {
    if (typeof this !== 'function') {
      throw new TypeError('Must be called on a function');
    }

    const self = this;
    return function (...innerArgs) {
      // context is the person object, innerArgs are the ones if you pass in the boundGreet, args are the ones you pass in greet.customBind(person, ....thisArgs)
      return self.apply(context, args.concat(innerArgs));
    };
  };
}

// Example usage:
function greet(name, age, occupation) {
  console.log(
    `Hello, my name is ${name} and I am ${age} years old. These are ${occupation} and I live in ${this.city}.`
  );
}
const person = { city: 'New York' };
const boundGreet = greet.customBind(person, 'Alice', 30);
boundGreet('Inner arguments'); // Output: Hello, my name is Alice and I am 30 years old. I live in New York.
```

</details>

---

**35. Implement a polyfill for `Array.map()` function**

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. map takes three parameters (element, index, array)
2. customMap should accept (arr, callback), callback is nothing but above three params
3. put a for loop to the arr
4. push the callback function into the result (ex: result.push(callback(three_params)))

```js
function customMap(arr, callback) {
  const result = [];

  for (let i = 0; i < arr.length; i++) {
    result.push(callback(arr[i], i, arr));
  }
  return result;
}
```

```js
const arr = [1, 2, 3, 4];
const doubleNums = customMap(arr, (element, index, originalArray) => {
  return element * 2;
});
```

</details>

---

**36. Implement a custom `Array.filter()` function**

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. filter takes three parameters (element, index, array)
2. customFilter should accept (arr, callback), callback is nothing but above three params
3. put a for loop to the arr
4. push the element into the result array only if the callback(three_params) is true (ex: result.push(callback(three_params)))

```js
function customFilter(arr, callback) {
  const result = [];

  for (let i = 0; i < arr.length; i++) {
    if (callback(arr[i], i, arr)) {
      result.push(arr[i]);
    }
  }
  return result;
}
```

```js
const arr = [1, 2, 3, 4];
const evenNums = customFilter(arr, (element, index, originalArray) => {
  return element % 2 === 0;
});
```

</details>

---

**37. WRITE SOMETHING HERE**

---

**38. Implement a custom `Array.of()` function**

```js
if (!Array.of) {
  Array.of = function () {
    // Create an empty array
    const arr = [];

    // Iterate over the arguments and push them into the array
    for (let i = 0; i < arguments.length; i++) {
      arr.push(arguments[i]);
    }

    // Return the newly created array
    return arr;
  };
}

// Tests
console.log(Array.of(1)); // [1]
console.log(Array.of(1, 2, 3)); // [1, 2, 3]
console.log(Array.of('a', 'b', 'c')); // ["a", "b", "c"]
```

---

**39. Implement a custom `Array.at()` function**

```js
if (!Array.prototype.at) {
  Array.prototype.at = function (index) {
    // If index is negative, calculate positive index from the end
    if (index < 0) {
      index = this.length + index;
    }

    // Return undefined for out of range indices
    if (index < 0 || index >= this.length) {
      return undefined;
    }

    // Return the item at the computed index
    return this[index];
  };
}

// Tests
const fruits = ['apple', 'banana', 'cherry', 'date'];
console.log(fruits.at(1)); // "banana"
console.log(fruits.at(-2)); // "cherry"
console.log(fruits.at(4)); // undefined
console.log(fruits.at(-5)); // undefined
```

---

**40. Implement a custom `Array.concat()` function**

```js
if (!Array.prototype.customConcat) {
  Array.prototype.customConcat = function () {
    // Create a new array to hold the concatenated result
    const result = [];

    // Start by pushing the current array's elements
    for (let i = 0; i < this.length; i++) {
      result.push(this[i]);
    }

    // Iterate over the arguments and append each of them to the result array
    for (let i = 0; i < arguments.length; i++) {
      const arg = arguments[i];

      // If the argument is an array, push its individual items
      if (Array.isArray(arg)) {
        for (let j = 0; j < arg.length; j++) {
          result.push(arg[j]);
        }
      } else {
        // If it's not an array, push the argument directly
        result.push(arg);
      }
    }

    // Return the concatenated array
    return result;
  };
}

// Tests
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
console.log(arr1.customConcat(arr2, 7, 8)); // [1, 2, 3, 4, 5, 6, 7, 8]
console.log(arr1.customConcat(9, [10, 11])); // [1, 2, 3, 9, 10, 11]
```

---

**41. Implement a custom `Array.fill()` function**

```js
if (!Array.prototype.customFill) {
  Array.prototype.customFill = function (value, start = 0, end = this.length) {
    // Handle negative indices
    if (start < 0) {
      start = this.length + start;
      start = start < 0 ? 0 : start; // Handle case where start is still negative
    }

    if (end < 0) {
      end = this.length + end;
    }

    // Fill the array with the given value from start to end index
    for (let i = start; i < end && i < this.length; i++) {
      this[i] = value;
    }

    return this;
  };
}

// Tests
const arr1 = [1, 2, 3, 4, 5];
console.log(arr1.customFill(0, 1, 4)); // [1, 0, 0, 0, 5]
const arr2 = [1, 2, 3, 4, 5];
console.log(arr2.customFill(8, -2)); // [1, 2, 3, 8, 8]
const arr3 = [1, 2, 3, 4, 5];
console.log(arr3.customFill(7)); // [7, 7, 7, 7, 7]
```

---

**42. Implement a custom `Array.join()` function**

```js
if (!Array.prototype.customJoin) {
  Array.prototype.customJoin = function (separator = ',') {
    // If the array is empty, return an empty string
    if (this.length === 0) {
      return '';
    }

    // Start with the first element as it won't be prefixed with the separator
    let result = String(this[0]);

    // Loop through the array starting from the second element
    for (let i = 1; i < this.length; i++) {
      result += String(separator) + String(this[i]);
    }

    return result;
  };
}

// Tests
const arr1 = ['apple', 'banana', 'cherry'];
console.log(arr1.customJoin()); // "apple,banana,cherry"
console.log(arr1.customJoin('-')); // "apple-banana-cherry"
console.log(arr1.customJoin(' and ')); // "apple and banana and cherry"
const arr2 = [];
console.log(arr2.customJoin()); // ""
const arr3 = [2, 4, 6, 8];
console.log(arr3.customJoin(':')); // "2:4:6:8"
```

---

**43. Implement a custom `Array.lastIndexOf()` function**

```js
if (!Array.prototype.customLastIndexOf) {
  Array.prototype.customLastIndexOf = function (
    searchElement,
    fromIndex = this.length - 1
  ) {
    // Handle negative indices
    if (fromIndex < 0) {
      fromIndex = this.length + fromIndex;
    }

    // Loop backwards starting from fromIndex
    for (let i = fromIndex; i >= 0; i--) {
      if (this[i] === searchElement) {
        return i;
      }
    }

    // If element not found, return -1
    return -1;
  };
}

// Tests
const arr1 = [2, 5, 9, 2];
console.log(arr1.customLastIndexOf(2)); // 3
console.log(arr1.customLastIndexOf(7)); // -1
console.log(arr1.customLastIndexOf(2, 3)); // 3
console.log(arr1.customLastIndexOf(2, 2)); // 0
console.log(arr1.customLastIndexOf(2, -2)); // 0
console.log(arr1.customLastIndexOf(2, -1)); // 3
```

---

**44. Implement a custom `Array.splice()` function**

```js
Syntax: splice(startIndex, deleteCount, item1, item2);
```

```js
- Time complexity: O(n)
- Space complexity: O(n)
```

```js
if (!Array.prototype.customSplice) {
  Array.prototype.customSplice = function (start, deleteCount, ...itemsToAdd) {
    // if the start/index parameter is negative, then we start counting from the end of the array
    if (start < 0) {
      //So, we adjust it by adding it to the array's length
      start = this.length + start;
      // starting point doesn't fall before the beginning of the array
      if (start < 0) start = 0;
    }

    // If deleteCount is not provided or it exceeds the length after start
    if (deleteCount === undefined || start + deleteCount > this.length) {
      // we ensure to adjust the deleteCount goes up to the end of the array
      deleteCount = this.length - start;
    }

    // Separate items to delete and to remain
    const removedItems = this.slice(start, start + deleteCount);

    // Construct the updated array
    const updatedArr = [
      //Taking all elements before the start index.
      ...this.slice(0, start),
      //Adding in the new items we want.
      ...itemsToAdd,
      //Adding all elements after the elements we deleted.
      ...this.slice(start + deleteCount),
    ];

    //emptying the original array
    this.length = 0;
    for (let item of updatedArr) {
      // we are pushing items from our `updatedArr` into the originalArray to modify it in place.
      this.push(item);
    }

    return removedItems;
  };
}

// Test
let arr = [1, 2, 3, 4, 5];
let removed = arr.customSplice(2, 2, 'a', 'b', 'c');
console.log(arr); // [1, 2, 'a', 'b', 'c', 5]
console.log(removed); // [3, 4]
```

---

**45. Implement a custom `String.charAt()` function**

```js
if (!String.prototype.customCharAt) {
  String.prototype.customCharAt = function (index = 0) {
    if (index < 0 || index >= this.length) {
      return '';
    }
    return this[index];
  };
}

// Tests
const str = 'Hello, world!';
console.log(str.customCharAt(0)); // "H"
console.log(str.customCharAt(7)); // "w"
console.log(str.customCharAt(50)); // ""
console.log(str.customCharAt(-1)); // ""
```

---

**46. Implement a custom `Promise.allSettled()` function**

```js
function customPromiseAllSettled(promises) {
  return new Promise((resolve) => {
    const results = [];
    let completedCount = 0;

    if (promises.length === 0) {
      resolve([]);
      return;
    }

    function checkCompletion() {
      completedCount++;
      if (completedCount === promises.length) {
        resolve(results);
      }
    }

    promises.forEach((promise, index) => {
      Promise.resolve(promise)
        .then((value) => {
          results[index] = { status: 'fulfilled', value };
          checkCompletion();
        })
        .catch((reason) => {
          results[index] = { status: 'rejected', reason };
          checkCompletion();
        });
    });
  });
}

// Example usage:
const promise1 = Promise.resolve(42);
const promise2 = Promise.reject('Error occurred');
const promise3 = new Promise((resolve) =>
  setTimeout(resolve, 1000, 'Delayed result')
);

customPromiseAllSettled([promise1, promise2, promise3])
  .then((results) => {
    console.log(results);
  })
  .catch((error) => {
    console.error(error);
  });
```

---

**47. Implement a custom `String.trim()` function**

```js
String.prototype.customTrim = function () {
  return this.replace(/^\s+|\s+$/g, '');
};

// Example usage:
const myString = '   Hello, world!   ';
const trimmedString = myString.customTrim();

console.log(trimmedString); // Output: "Hello, world!"
```

---

**48. Implement `Object.is()` function**

```js
//Example
// Object.is() is similar to === except following cases

Object.is(0, -0); // false
0 === -0; // true

Object.is(NaN, NaN); // true
NaN === NaN; // false
```

```js
if (!Object.customIs) {
  Object.customIs = function (x, y) {
    // Handle the special case of NaN
    if (x !== x && y !== y) {
      return true;
    }

    // Handle the special case of +0 and -0
    if (x === 0 && y === 0) {
      return 1 / x === 1 / y;
    }

    // For all other cases, use ===
    return x === y;
  };
}

// Tests
console.log(Object.customIs(42, 42)); // true
console.log(Object.customIs('foo', 'foo')); // true
console.log(Object.customIs(false, false)); // true
console.log(Object.customIs(NaN, NaN)); // true
console.log(Object.customIs(+0, -0)); // false
console.log(Object.customIs(-0, -0)); // true
console.log(Object.customIs('foo', 'bar')); // false
console.log(Object.customIs([], [])); // false (different references)
```

---

**49. Implement `Promise.prototype.finally()` function**

```js
//Example
Promise.prototype.finally() could be used to run a callback when a promise is settled(either fulfilled or rejected).

Notice that the callback passed finally() doesn't receive any argument, meaning it doesn't modify the value in the promise chain (care for rejection).
```

```js
if (typeof Promise !== 'undefined' && !Promise.prototype.customFinally) {
  Promise.prototype.customFinally = function (callback) {
    const P = this.constructor; // Get the Promise constructor

    // We don’t invoke the callback in here, we just make sure to propagate
    // the value of the original Promise once it's resolved
    return this.then(
      (value) => P.resolve(callback()).then(() => value),
      (reason) =>
        P.resolve(callback()).then(() => {
          throw reason;
        })
    );
  };
}

// Test cases
const successPromise = Promise.resolve('Success!');
const failPromise = Promise.reject('Failure!');

successPromise
  .then((value) => console.log(value))
  .catch((err) => console.log('Error:', err))
  .customFinally(() => console.log('Final callback for successPromise'));

failPromise
  .then((value) => console.log(value))
  .catch((err) => console.log('Error:', err))
  .customFinally(() => console.log('Final callback for failPromise'));
```

```js
//Output:
Success!
Error: Failure!
Final callback for successPromise
Final callback for failPromise
```

---

**50. Implement `Array.prototype.sort()` function**

```js
Array.prototype.customSort = function (compareFunction) {
  // This checks if a compareFunction is provided and if it is of type 'function'
  if (typeof compareFunction !== 'function') {
    // numbers.customSort(), strings.customSort({}) are the few examples for compareFunction!=='function'
    compareFunction = (a, b) => {
      if (a === b) return 0;
      return a < b ? -1 : 1;
    };
  }

  const merge = (left, right) => {
    let result = [];
    let indexLeft = 0;
    let indexRight = 0;

    while (indexLeft < left.length && indexRight < right.length) {
      const comparison = compareFunction(left[indexLeft], right[indexRight]);

      if (comparison <= 0) {
        // If the result is less than or equal to 0, it means the left element should come first,
        result.push(left[indexLeft]);
        indexLeft++;
      } else {
        //otherwise, the right element should come first.
        result.push(right[indexRight]);
        indexRight++;
      }
    }

    //result is the array where the sorted elements will be pushed.
    // These lines add any remaining elements to the result array.
    return result.concat(left.slice(indexLeft), right.slice(indexRight));
  };

  //This recursive function sorts an array.
  const mergeSort = (array) => {
    // If the array has one or zero elements, it just returns the array because it is already sorted.
    if (array.length <= 1) {
      return array;
    }

    const middle = Math.floor(array.length / 2);
    const left = array.slice(0, middle);
    const right = array.slice(middle);

    return merge(mergeSort(left), mergeSort(right));
  };

  const sortedArray = mergeSort(this);
  for (let i = 0; i < this.length; i++) {
    //The sorted elements are then copied from sortedArray back to the original array.
    this[i] = sortedArray[i];
  }

  //Finally, the sorted array is returned.
  return this;
};

// Usage
let numbers = [5, 3, 8, 1, 2];
numbers.customSort((a, b) => a - b);
console.log(numbers); // [1, 2, 3, 5, 8]

let strings = ['banana', 'apple', 'orange', 'grapes'];
strings.customSort();
console.log(strings); // ['apple', 'banana', 'grapes', 'orange']
```

---
