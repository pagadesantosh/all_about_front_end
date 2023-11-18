## DeepClone of an object

- <strong>Approach Taken :</strong>

1. An input obj can have an object or null or an array
2. Write three conditions, one for handling objects, arrays, (null and not object)
3. If it is not object (ex: a: 6), then return as it is (i.e the obj passed)
4. If it is array, map with each and every item and pass that item into the function (Which will satisfy one of the three conditions)
5. If it is an object, use a `for-in` loop to iterate inside the object and for each property of the source object (obj), it calls the deepClone function recursively

```js
function deepClone(obj) {
  // Handle primitive types and null
  if (obj === null || typeof obj !== 'object') return obj;

  // Handle arrays
  if (Array.isArray(obj)) {
    return obj.map((item) => deepClone(item));
  }

  // Handle objects
  const copy = {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      copy[key] = deepClone(obj[key]);
    }
  }
  return copy;
}

// Example usage:
const obj = {
  a: 1,
  b: {
    c: 2,
    d: {
      e: 3,
    },
  },
  f: [4, 5, { g: 6 }],
};

const deepClonedObj = deepClone(obj);
const shallowClonedObj = Object.assign({}, obj);

console.log('deepClonedObj', deepClonedObj); // { a: 1, b: { c: 2, d: { e: 3 } }, f: [ 4, 5, { g: 6 } ] }

console.log('shallowClone', shallowClonedObj); // { a: 1, b: { c: 2, d: { e: 3 } }, f: [ 4, 5, { g: 6 } ] }

console.log('deepClonedObj', deepClonedObj.b.d === obj.b.d); //false

console.log('shallowClonedObj', shallowClonedObj.b.d === obj.b.d); //true
```
