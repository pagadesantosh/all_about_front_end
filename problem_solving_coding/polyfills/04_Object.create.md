## Object.create:

**Definition:** Is used to create a new object using an existing object as the prototype of the newly created object.

```js
//Syntax
Object.create(proto, propertiesObject);
```

<strong>Approach Taken:</strong>

```js
function createObject(proto) {
  Object.prototype.customCreate = function (proto) {
    if (proto === null || typeof proto !== 'object') {
      throw new Error('Argument must be the object, or null');
    }
    //empty function
    function F() {}
    //prototype chaining with proto as the value
    F.prototype = proto;
    //return the new Function
    return new F();
  };
}

const obj1 = {
  key: 1,
  sayHello() {
    return 'Hello';
  },
};

const newObj1 = Object.customCreate(obj1);
console.log('newObj1', newObj1);
console.log('newObj1 Key', newObj1.key);
console.log('newObj1 sayHello', newObj1.sayHello());
```

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/c47e3ec6-5e28-4e7b-a72d-46f725f19064)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/3d79a21f-39fd-43d3-871a-a1ecd9e3a5c3)
