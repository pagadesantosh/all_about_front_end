1) What is a promise?
2) when to use callback and when to use promise?
3) Output based question
const object1 = {
  a: 10,
  b: 20,
  c: function () {
    console.log(this.a + this.b);
  },
};
const func = object1.c;
func();

4) Output based question
const array = [1,2,3]
array=[4,5,6]

5) What is react and Why to use react ?
6) Component Life Cycles of React?
7) HTML events vs React events?
8) React fiber?
9) input and output in node.js ?
10) event driven programming in node.js ?
11) npm ?

---- 

12) How does function is being executed in Javascript?

-----

### 13) inheritance in javascript?
- JavaScript uses <ins>**prototypal inheritance**</ins>, a different approach compared to the classical inheritance model seen in languages like `Java` or `C++`. 
- In JavaScript, <ins>**`objects` inherit directly from other objects**</ins>.


- **Prototype Chain**: 
  - <ins>**Every JavaScript object has a prototype property (except for the base object)**</ins>, which is a reference to another object. 
  - When a property or method is accessed, JavaScript will look up the property on the object itself first; <ins>**if it doesn’t find it, it continues to look up the chain in the object’s prototype**</ins>.
  <br/>

- **Creating Inheritance**: 
  - You can <ins>**establish inheritance by setting the prototype of a constructor function or class to be an instance of another constructor function.** </ins>
  - This allows the derived object to inherit methods and properties from the base object.

```js
// Using Constructors and Prototypes:

function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function() {
  console.log(`${this.name} makes a noise.`);
};

function Dog(name) {
  Animal.call(this, name); // Super constructor call
}

// ensure that instances of `Dog` inherit properties and methods from `Animal`
Dog.prototype = Object.create(Animal.prototype);

//we ensure that the constructor reference on instances of Dog
// correctly points back to Dog itself, not Animal
// 
Dog.prototype.constructor = Dog;

Dog.prototype.speak = function() {
  console.log(`${this.name} barks.`);
};

let dog = new Dog('Rex');
dog.speak();  // Outputs: Rex barks.
```
---

```js
//Using ES6 Classes:

class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks.`);
  }
}

let dog = new Dog('Rex');
dog.speak();  // Outputs: Rex barks.
```

----

### 14. Post vs put

#### i) POST Method
- **Purpose**: 
  - The POST method is **used to <ins>create a new resource on the server**</ins>.
- **Idempotence**: 
  - POST is a non-idempotent method. This means that multiple identical POST requests <ins>**can result in different outcomes**</ins> or the creation of multiple entries.
- **Usage**: 
  - You would use POST **when you want <ins>to add a new entry to a database**</ins>. 

- *For example*, 
  - <ins>adding a new user to an application</ins>, 
  - <ins>submitting a form</ins>, 
  - <ins>or uploading a file</ins>.
- **Data Handling**: 
  - Data sent via POST is typically <ins>**included in the body of the request**</ins>. 
  - This can be in various formats such as `JSON`, `FormData`, `XML`, etc.

```js
// EXAMPLE OF POST REQUEST (fetch and promises)

fetch('https://api.example.com/items', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        name: 'New Item',
        description: 'Detailed description here'
    })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```


```js
// EXAMPLE OF POST REQUEST (axios and async-await)

// Import axios
import axios from 'axios';

async function createNewItem() {
    try {
        const response = await axios.post('https://api.example.com/items', {
            name: 'New Item',
            description: 'Detailed description here'
        });
        console.log('Created Item:', response.data);
    } catch (error) {
        console.error('Error creating item:', error);
    }
}

// Call the function to execute the POST request
createNewItem();
```

#### ii) PUT Method
- **Purpose**: 
  - The `PUT` method is used <ins>**to update an existing resource or create a new resource if it does not exist**</ins>, at a specific URL.
- **Idempotence**: 
  - `PUT` <ins>is an `idempotent` method</ins>. 
  - This means that **making multiple identical PUT requests will <ins>always result in the same state of the resource</ins>** after the requests are made, essentially updating the resource.
- **Usage**: 
  - Use `PUT` <ins>**when you are updating an entire resource or replacing it entirely**</ins>. 
  - For example, 
    - <ins>updating a user's profile information</ins> 
    - <ins>or replacing the contents of a file</ins>. 
- **Data Handling**: 
  - Like POST, <ins>the data for PUT requests is also typically **included in the body of the request**</ins>.

```js
fetch('https://api.example.com/items/123', {
    method: 'PUT',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        name: 'Updated Item',
        description: 'Updated description here'
    })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```


```js
// EXAMPLE OF POST REQUEST (axios and async-await)

// Import axios
import axios from 'axios';

async function updateItem() {
    try {
        const response = await axios.put('https://api.example.com/items/123', {
            name: 'Updated Item',
            description: 'Updated description here'
        });
        console.log('Updated Item:', response.data);
    } catch (error) {
        console.error('Error updating item:', error);
    }
}

// Call the function to execute the PUT request
updateItem();
```




**Verdict**: Selected
