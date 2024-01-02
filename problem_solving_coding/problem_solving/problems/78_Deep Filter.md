### Deep Filter with result as object

```js
//input is the object, callback is based on how you want to filter the element (ex: element > 0)
function filter(input, callback) {
  const result = {};

  // initially you would only get the keys of non-nested ones (ex: a, b in our first example)
  Object.keys(input).forEach((key) => {
    // storing the values of the keys (ex: a: 1, b: Object{})
    const value = input[key];

    // if type is of object
    if (typeof value === 'object' && value !== null) {
      // recursion
      const filteredObject = filter(value, callback);
      // if there are keys in the above filtered object
      if (Object.keys(filteredObject).length > 0) {
        // store that key in the result object with value as filteredObject
        result[key] = filteredObject;
      }
      // if type is not of object and adhering to callback (ex: element > 0)
    } else if (callback(value)) {
      // store that key in the result object with value
      result[key] = value;
    }
  });

  // don't forget to return the end result object
  return result;
}

// Example usage
const input1 = {
  a: 1,
  b: {
    c: 2,
    d: -3,
    e: {
      f: {
        g: -4,
      },
    },
    h: {
      i: 5,
      j: 6,
    },
  },
};

const callback1 = (element) => element >= 0;
const filtered1 = filter(input1, callback1);
console.log(filtered1); // { a: 1, b: { c: 2, h: { i: 5, j: 6 } } }

const input2 = {
  a: 1,
  b: {
    c: 'Hello World',
    d: 2,
    e: {
      f: {
        g: -4,
      },
    },
    h: 'Good Night Moon',
  },
};

const callback2 = (element) => typeof element === 'string';
const filtered2 = filter(input2, callback2);
console.log(filtered2); // { b: { c: 'Hello World', h: 'Good Night Moon' } }
```
