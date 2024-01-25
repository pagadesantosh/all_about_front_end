- As we know that **_arrays and functions are nothing but objects_** in javascript.
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/4a5db691-9da7-473e-9383-e4abca54b390)
- Javascript uses prototypical inheritance, By this means **_array object/function object gets access to their properties and methods_** of the object through this prototypical inheritance

###### There is a way to see this prototype chain (using double underscore proto)

**Arrays:**
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/4dacbba0-eba7-462a-b4eb-acfe4ac664e9)

**Functions:**
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/47301e2e-952f-43d5-a86d-22f59dce8b42)

**Object**
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/93e92558-2b2d-4e7d-84ed-5041c00d4f20)

<u>**Let's go through few examples:**</u>

```js
// Object 1
let dragon = {
  fire: true,
  name: 'Tanya',
  fight() {
    return 5;
  },
  sing() {
    return `I'm ${this.name}, the breather of fire`;
  },
};

console.log(dragon.fight()); //5
console.log(dragon.sing()); //I'm Tanya, the breather of fire
```

```js
// Object 2
let lizard = {
  name: 'Kiki',
  fight() {
    return 1;
  },
};
```

- Let's say if we **_wanted to borrow sing method_** from the dragon object, one of the way is to **_call/apply/bind_**

```js
let singLizard = dragon.sing.bind(lizard);
console.log(singleLizard()); // I'm Kiki, the breather of fire
```

- Above logic **_works totally fine for the object 1_**, but what if our dragon object gets a little more complicated

---

<u>**What if the object gets more complicated:**</u>

```js
// Updated Object 1, added if condition to the sing method
let dragon = {
  fire: true,
  name: 'Tanya',
  fight() {
    return 5;
  },
  sing() {
    if (this.fire) {
      return `I'm ${this.name}, the breather of fire`;
    }
  },
};
```

```js
// Object 2, as it was
let lizard = {
  name: 'Kiki',
  fight() {
    return 1;
  },
};
```

```js
//trying to bind to the updated dragon object
let singleLizard = dragon.sing.bind(lizard);
console.log(singleLizard()); // undefined

//because lizard object doesn't have fire property set to true
// even though we borrow the method, we don't have the fire accessibility in this case, so it is never going to be surpass if condition.
```

---

#### This is where prototypical inheritance comes in 😎

- What if we create a prototype chain **_so that lizard(object 2) inherit all the properties and methods of dragon(object 1)_**

```js
// Updated Object 1, as per above
let dragon = {
  fire: true,
  name: 'Tanya',
  fight() {
    return 5;
  },
  sing() {
    if (this.fire) {
      return `I'm ${this.name}, the breather of fire`;
    }
  },
};
```

```js
// Object 2, as it was
let lizard = {
  name: 'Kiki',
  fight() {
    return 1;
  },
};
```

```js
lizard.__proto__ = dragon;
lizard.sing(); //"I'm Kiki, the breather of fire"
```

```js
lizard.fire; // true
```

```js
lizard.fight; // 1
```

**_What we were able to do here is, `inherit all the properties and methods of dragon object(Object 1)` + whatever the properties we define in our lizard(Object 2) will stay with us_**

```js
//isPrototypeOf is being checked in the Dragon Object prototype chain,
// does lizard inherit the properties from dragon?
dragon.isPrototypeOf(lizard); //true
```

---

<u>**Looping through the object:**</u>

```js
// Object 1
let dragon = {
  fire: true,
  name: 'Tanya',
  fight() {
    return 5;
  },
  sing() {
    if (this.fire) {
      return `I'm ${this.name}, the breather of fire`;
    }
  },
};

// Object 2, as it was
let lizard = {
  name: 'Kiki',
  fight() {
    return 1;
  },
};

lizard.__proto__ = dragon;

for (let prop in lizard) {
  console.log(prop);
}

// Output
name;
fight;
fire;
sing;
```

---

<u>**Looping through the object:**</u>

<b>`using hasOwnProperty`:</b>

```js
// Object 1, as it was
let dragon = {
  fire: true,
  name: 'Tanya',
  fight() {
    return 5;
  },
  sing() {
    if (this.fire) {
      return `I'm ${this.name}, the breather of fire`;
    }
  },
};

// Object 2, as it was
let lizard = {
  name: 'Kiki',
  fight() {
    return 1;
  },
};

lizard.__proto__ = dragon;

for (let prop in lizard) {
  //added if condition
  if (lizard.hasOwnProperty(prop)) {
    console.log(prop);
  }
}

// Output
name;
fight;
```

<u>**Note:**</u> Never use **_double underscore proto_** 😄

<u>**Why Prototypical Inheritance is useful:**</u>

- The fact that objects can share prototypes means that you can have **_objects with properties & methods that are pointing to the same place in memory_**, thus being memory efficient.

- Instead of copying the same functionality in different places in memory, **_we have it in just at one place_**

---

##### Objects

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/79a8a574-ee80-468f-92e5-a24ff71a12ca)

##### Functions

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/2857a213-49d3-41bb-a213-1b1b78a085b7)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/73d39ab0-dbab-4772-9e3e-4a3b7090c395)

**_proto links to prototype_**

- _proto is simply a reference or a pointer to Prototype Object_
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/3f3dfcff-a206-461d-aad6-4bedbd37a0ca)

**_proto links up to the Function()_**
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/4c31909f-514a-4812-8186-f33b90dfdae1)

**WHAT IS HAPPENING**
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/f45ee734-6513-4198-858a-e4c1a96aea8d)

##### Functions

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/5970a307-c29d-40ec-9914-5fc09f027146)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/4089d2a4-66ca-41b5-9e4d-11fb1e17bd32)

##### Arrays

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/66485063-c529-45a8-a5d1-19ce25dacc13)

<u>**One thing to remember is:**</u> **_double underscore proto_** property actually **_lives on the prototype_**

---

Safe way to create own prototypes is by using Object.create()

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/e281f985-1bd1-4516-a110-b0ad66fde5a4)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/12437a00-af2d-40c3-be35-067f53c50621)

**_In Functions, The only time when we use prototypes is when we call constructor functions._**

- Constructor functions usually start with a capital letter and they contain the prototype that we use

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/c6aecbca-bc7b-49e1-8050-868d6c3f2091)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/31b14a56-03e6-4fc2-b817-a706144cb6e8)

```js
typeof Object; //'function'
```

<u>**One thing to remember is:**</u> Every function has a prototype property and it references to an object used to attach properties that will be inherited by objects further down the prototype chain. The last object in the chain is this built in object (Object.prototype)

<u>**Another thing to remember is:**</u> **_Object_** is a function because it has the prototype and now Object.prototype is what we call the base object

**WHAT IS HAPPENING**
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/7254867f-2f2f-4a56-bb64-788456650e9a)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/56ef4b9c-fdc1-43c5-a988-8ba77a3c76be)

**Only Functions have prototypes**
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/dd881eb1-6840-4cf9-840b-eea18ffe0b88)

<u>**Summary:**</u>
Using prototypes, we avoid repeating ourselves. We avoid adding the same code over and over and over and being inefficient with our memory.

---

<u><b>Interview Question:</b></u> Difference between proto and prototype

`__proto__`:

- `__proto__` is a property of an object **_that points to the prototype of the constructor function_** which created that object.
- It is a part of the internal prototype chain that Javascript uses to look up properties and methods
- is the actual object that is used in the lookup chain to resolve methods
- Direct use of proto is discouraged, Instead the standard functions Object.setPrototypeOf and Object.getPrototypeOf are recommended

`prototype:`

- prototype is a **_property of a function object_**, <u>specifically a constructor function</u>, that is used to set the prototype of new objects created with that constructor function
- Ex: if you have a constructor function `MyConstructor`, MyConstructor.prototype will be the object that new instances created with new MyConstructor will have in their `__proto__`

```js
//Sample Code
function MyConstructor() {}

MyConstructor.prototype.addSomeFunc = function () {};

const newInstance = new MyConstructor();

console.log(newInstance.__proto__ === MyConstructor.prototype); //true
```

#### Refer below screenshot from browser console

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/a16d60d1-1fad-4cfa-8c8e-114d8f1f5deb)

---

### Another scenarios:

```js
const myObject = { channelName: 'JsCafe' };
console.log(myObject.channelName); // JsCafe
console.log(myObject.hasOwnProperty('channelName')); //true

function myFunction() {
  console.log('Welcome to JsCafe');
}

myFunction.color = 'red';
console.log(myFunction()); //
console.log(myFunction.color); //red
console.log(myFunction.toString()); // prints myFunction as it is
console.log(myFunction.hasOwnProperty('color')); //true
```

---

<strong>Global memory</strong>: Space of memory in browser or in JS engine where `javascript stores variables and functions`.

- When Javascript scans the whole code, it stores the objects and functions in the global memory.

```js
//Example for the above code snippet, the global memory looks like below
myObject: {
  channelName: 'JsCafe';
}
myFunction: f;
```

- Javascript by default adds the property called prototype (for Objects and for Functions) which is again an object (and in this prototype object we have a property named as hasOwnProperty which is a function), some others are like toLocaleString()
- Similarly there are other properties like toLocaleString (which is also a function)
- For every object, Javascript by default adds one more property called `proto`
- Labelled as Object and for this particular function, `proto` points to null

Ex: For myObject by default javascript adds the `proto` property and this points out to the prototype of the Object Function

- So whenever a function is created in javascript it is just not a function but it is a bundle of function and object both.

Ex: myFunction is a function + object which has color property and `proto` (whereas this `proto` property points out to )

![image](https://user-images.githubusercontent.com/42731246/215369453-f30b0815-9ca2-4fe9-b869-6f62706970af.png)

- For the myFunction when we perform hasOwnProperty then the Javascript finds the hasOwnProperty inside the Object (look out the proto mapping)

---

### Few more

### Prototypical Inheritance and Prototype Chain

- ES6 introduced classes which is a modern way to construct objects
- ES6 classes are considered to be syntactic sugar

#### Example 1

```js
// Object literals
const person = {
  alive: true,
};

const musician = {
  plays: true,
};

console.log(musician.plays); //true
console.log(musician.alive); //undefined
```

---

#### Example 2 (adding proto property)

- This is happening through inheritance
- person object is the parent/proto of the musician object

```js
// Object literals
const person = {
  alive: true,
};

const musician = {
  plays: true,
};

musician.__proto__ = person;

console.log(musician.plays); //true
console.log(musician.alive); //true
```

- If you try to log the musician object in this case, it is something looks like below
- Also if you expand the Javascript Object (you would find out the proto is nothing but getter and setter)
- This is the old way of setting the prototype

### ADD Screenshot here

---

#### New way of setting the Prototype instead of proto (getPrototypeOf, setPrototypeOf)

```js
//person object is the prototype for the musician object
Object.setPrototypeOf(musician, person);

console.log(Object.getPrototypeOf(musician)); // {alive:true}
console.log(musician.__proto__); // {alive:true}
console.log(Object.getPrototypeOf(musician) === musician.__proto__); // true
```

---

#### Important points to note down:

- After setting the prototype for an object (ex: setting the person object as a prototype to the musician object) in above scenario

- If we try to log out the property which is not available in the musician object then javascript looks for the alive property in the musician and if it is not there it goes to the next link of the prototype chain to the person object (musician proto) and there you can see the alive property is found.
- In some cases the property like (hasOwnProperty) is called then Javascript looks this property inside the Javascript Object(this is the parent of all the objects)

```js
//Extending the prototype chain

const guitarist = {
  strings: 6,
  __proto__: musician,
};

console.log(guitarist);
```

### ADD Screenshot here

---

- #### No circular references are allowed

```js
// person.__proto__ can't be guitarist
```

- #### The proto value must be object or null
- #### An object can only directly inherit from one object

---

#### Example 3 (object with getter and setter methods)

```js
const car = {
  doors: 2,
  seats: 'vinyl',
  get seatMaterial() {
    return this.seats;
  },
  set seatMaterial(material) {
    this.seats = material;
  },
};

const luxuryCar = {};
Object.setPrototypeOf(luxury, car); // car object is the prototype
luxuryCar.seatMaterial = 'leather';
console.log(luxuryCar); //{seats: "leather"}
console.log(luxuryCar.doors); // 2
console.log(car); // {doors: 2, seats: "vinyl"}
```

---

#### Example 4 (Walking up the chain)

- valueOf method is actually present in the Javascript Object

```js
// props and methods are not copied

console.log(luxuryCar.valueOf()); // {seats: "leather"}
```

---

#### Example 5 (Getting the keys of an object)

- logs an array

```js
console.log(Object.keys(luxuryCar)); // ["seats"]
```

---

#### Example 6 (loop through each object key)

- logs a item

```js
Object.keys(luxuryCar).forEach((key) => console.log(key)); // seats
```

---

#### Example 7 (for in loop includes inherited props also)

- logs keys that are inherited

```js
for (let key in luxuryCar) {
  console.log(key);
}

//Output:
seats;
doors;
seatMaterial;
```

---

#### Example 8 (Object Constructors)

- The prototype property is where inheritable props and methods are

```js
function Animal(species) {
  this.species = species;
  this.eats = true;
}

Animal.prototype.walks = function () {
  return `A ${this.species} is walking`;
};

const Bear = new Animal('bear');
console.log(Bear.species); // bear
console.log(Bear.walks()); // A bear is walking
console.log(Bear.__proto__ === Animal.prototype); // true
```

---

#### Example 9 (ES6 classes as a example of inheritance)

- The beauty of this prototype inheritance is we are not changing the parent properties
- myBike and myTruck are the examples

```js
class Vehicle {
  constructor() {
    (this.wheels = 4), (this.motorized = true);
  }
  ready() {
    return 'Ready to go!';
  }
}
```

```js
class Motorcycle extends Vehicle {
  constructor() {
   super()
   this.wheels = 2,
  }
  wheelie() {
    return 'On one wheel now!'
  }
}

const myBike = new Motorcycle()
console.log(myBike) // {wheels:2, motorized: true}
console.log(myBike.wheels) // 2
console.log(myBike.ready()) // Ready to go!
console.log(myBike.wheelie()) // On one wheel now!


const myTruck = new Vehicle()
console.log(myTruck) // {wheels: 4, motorized: true}
```

#### If we try to log myTruck

## ![image](https://user-images.githubusercontent.com/42731246/217040382-bef8257e-57c6-4e36-abdb-4c744e4b7511.png)
