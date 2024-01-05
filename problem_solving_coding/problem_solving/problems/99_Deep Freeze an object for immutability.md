```js
function deepFreeze(object) {
  // Retrieve the property names defined on object
  const propNames = Object.getOwnPropertyNames(object);

  // Freeze properties before freezing self
  for (const name of propNames) {
    //ex: value variable below results with 'value1' for property1 name
    const value = object[name];

    // If value is an object, freeze it too
    if (value && typeof value === 'object') {
      deepFreeze(value);
    }
  }

  return Object.freeze(object);
}

// Example usage
const myObject = {
  property1: 'value1',
  nestedObject: {
    property2: 'value2',
    innerNestedObject: {
      property3: 'value3',
    },
  },
};

deepFreeze(myObject);

// Trying to modify the object will have no effect
myObject.property1 = 'new value';
myObject.nestedObject.property2 = 'new value';
myObject.nestedObject.innerNestedObject.property3 = 'new value';

console.log(myObject); // The object and its nested objects remain unchanged
```
