```js
function deepFreeze(myObject) {
  for (let key in myObject) {
    if (myObject.hasOwnProperty(key)) {
      const value = myObject[key];
      if (typeof value === 'object') {
        deepFreeze(value);
      }
    }
  }
  return Object.freeze(myObject);
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

console.log(deepFreeze(myObject));

myObject.property1 = 'new value';
myObject.nestedObject.property2 = 'new value';
myObject.nestedObject.innerNestedObject.property3 = 'new value';
console.log('After', deepFreeze(myObject));

/*
Output:
{
  property1: 'value1',
  nestedObject: { property2: 'value2', innerNestedObject: { property3: 'value3' } }
}
After {
  property1: 'value1',
  nestedObject: { property2: 'value2', innerNestedObject: { property3: 'value3' } }
}
*/
```
