## Object.create:

**Definition:** Is used to create a new object using an existing object as the prototype of the newly created object.

```js
//Syntax
Object.create(proto, propertiesObject);
```

<strong>Approach Taken:</strong>

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
