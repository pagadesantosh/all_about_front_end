### Prototypical Inheritance and Prototype Chain

- ES6 introduced classes which is a modern way to construct objects
- ES6 classes are considered to be syntactic sugar

#### Example 1

```js
// Object literals
const person = {
  alive: true,
}

const musician = {
  plays: true,
}

console.log(musician.plays) //true
console.log(musician.alive) //undefined
```

---

#### Example 2 (adding proto property)

- This is happening through inheritance
- person object is the parent/proto of the musician object

```js
// Object literals
const person = {
  alive: true,
}

const musician = {
  plays: true,
}

musician.__proto__ = person

console.log(musician.plays) //true
console.log(musician.alive) //true
```

- If you try to log the musician object in this case, it is something looks like below
- Also if you expand the Javascript Object (you would find out the proto is nothing but getter and setter)
- This is the old way of setting the prototype

### ADD Screenshot here

---

#### New way of setting the Prototype instead of proto (getPrototypeOf, setPrototypeOf)

```js
//person object is the prototype for the musician object
Object.setPrototypeOf(musician, person)

console.log(Object.getPrototypeOf(musician)) // {alive:true}
console.log(musician.__proto__) // {alive:true}
console.log(Object.getPrototypeOf(musician) === musician.__proto__) // true
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
}

console.log(guitarist)
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
  seats: "vinyl",
  get seatMaterial() {
    return this.seats
  },
  set seatMaterial(material) {
    this.seats = material
  },
}

const luxuryCar = {}
Object.setPrototypeOf(luxury, car) // car object is the prototype
luxuryCar.seatMaterial = "leather"
console.log(luxuryCar) //{seats: "leather"}
console.log(luxuryCar.doors) // 2
console.log(car) // {doors: 2, seats: "vinyl"}
```

---

#### Example 4 (Walking up the chain)

- valueOf method is actually present in the Javascript Object

```js
// props and methods are not copied

console.log(luxuryCar.valueOf()) // {seats: "leather"}
```

---

#### Example 5 (Getting the keys of an object)

- logs an array

```js
console.log(Object.keys(luxuryCar)) // ["seats"]
```

---

#### Example 6 (loop through each object key)

- logs a item

```js
Object.keys(luxuryCar).forEach((key) => console.log(key)) // seats
```

---

#### Example 7 (for in loop includes inherited props also)

- logs keys that are inherited

```js
for (let key in luxuryCar) {
  console.log(key)
}

//Output:
seats
doors
seatMaterial
```

---

#### Example 8 (Object Constructors)

- The prototype property is where inheritable props and methods are

```js
function Animal(species) {
  this.species = species
  this.eats = true
}

Animal.prototype.walks = function () {
  return `A ${this.species} is walking`
}

const Bear = new Animal("bear")
console.log(Bear.species) // bear
console.log(Bear.walks()) // A bear is walking
console.log(Bear.__proto__ === Animal.prototype) // true
```

---

#### Example 9 (ES6 classes as a example of inheritance)

- The beauty of this prototype inheritance is we are not changing the parent properties
- myBike and myTruck are the examples

```js
class Vehicle {
  constructor() {
    ;(this.wheels = 4), (this.motorized = true)
  }
  ready() {
    return "Ready to go!"
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
