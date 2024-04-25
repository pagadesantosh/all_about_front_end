### 1. How would you achieve the output ?

```js
let mixin = {
    sayHi() {
        console.log(`Hello ${this.name}`);
    },
    sayBye() {
        console.log(`Bye ${this.name}`);
    },
};

class User {
    constructor(name) {
        this.name = name;
    }
}
let user = new User("John");
user.sayHi(); // Hello John
user.sayBye(); // Bye John
```

----

### 2. Will this code work ?
```js
function f(phrase) {
  return class {
    sayHi() {
      console.log(phrase);
    }
  };
}

class User extends f('Hello') {}

new User().sayHi();
```
----

### 3. HOC
- Why it is required?
- How to write multiples HOCs in a regular component?

----

### 4. Why do we need constructors? can we create classes without constructors

- `Yes`, <ins>**you can create** classes without constructors</ins> in JavaScript
<br/>

- In JavaScript, <ins>if a class does not have a constructor explicitly defined, **it automatically uses a default constructor**</ins>.

#### 1. JavaScript Classes Without Constructors:

```js
// MyClass does not have a constructor, 
// but it can still be instantiated, and its method can be called.
class MyClass {
    method() {
        console.log('Hello, World!');
    }
}

const myInstance = new MyClass();
myInstance.method(); // Outputs: Hello, World!
```

#### 2. React Component Classes Without Constructors:
- Similarly, in React, <ins>**you can define class components without constructors</ins>**. 
- State and props can still be managed, though it's more common to see constructors used when there is a need to initialize state or bind methods.

---

### 5. how to implement pagination