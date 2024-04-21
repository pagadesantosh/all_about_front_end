## 1. How would you achieve the output ?

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



## 2. Will this code work ?
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

## 3. HOC
- Why it is required?
- How to write multiples HOCs in a regular component?