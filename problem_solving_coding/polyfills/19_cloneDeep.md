## cloneDeep

**Definition**: Loadash.cloneDeep() method is used to `create a deep copy` of the value and it `recursively clones` the value. The newly created object has the `same value as the original` but they are `not the same object in the memory`.

<strong>Approach Taken:</strong>

1. one condition for primitives and null (ex: typeof value!==object || value === null)
2. one condition for Array.isArray(value)
3. another condition for typeof value === 'object'
4. for primitives & null (I mean for condition 1), simply return the param that you have passed (ex: value)
5. for Array condition, write a basic for loop based on the value.length. Maintain an array for recursion (ex: finalArr[i] = cloneDeep(value[i])). Post for loop ends, return that stored/created finalArr
6. for object condition, maintain an empty object and perform a for-in-loop and pass recursively (ex: finalObj[key] = cloneDeep(value[key])). Post for loop ends, return the finalObj

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
