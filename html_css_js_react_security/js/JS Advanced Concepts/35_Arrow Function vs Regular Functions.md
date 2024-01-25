```js
class Person {
  constructor(name) {
    this.name = name
  }

  printNameArrow() {
    setTimeout(() => {
      console.log("Arrow" + this.name)
    }, 100)
  }

  printNamedFunction() {
    setTimeout(function () {
      console.log("Function" + this.name)
    }, 100)
  }
}

let person = new Person("Bob")
person.printNameArrow()
person.printNamedFunc()
console.log(this.name)
```

<details>
<summary>Solution</summary>

```js
// ReferenceError: Cannot access 'letVar' before initialization
```

```js
3rd console.log prints nothing
1st console.log Arrow Bob
Function
```

</details>

#### Example 1 (better to use Arrow Functions in this case)

```js
// this and e.target are exactly the same in Regular function
document.addEventListener("click", function (e) {
  console.log("Regular Function", this, e.target)
})

// this keyword in Arrow defaults to the outer context, for ex: Window
document.addEventListener("click", (e) => {
  console.log("ARROW Function", this, e.target)
})
```

#### Example 2 (better to use Regular Functions in this case)

- this in the below case is window

```js
const person = {
  firstName: "Kyle",
  lastName: "Cook",
  printName: () => {
    console.log(`${this.firstName}${this.lastName}`)
  },
}

person.printName()
```

<details>
<summary>Solution</summary>

```js
undefined undefined
```

</details>

---

- this in the below case is window

```js
const person = {
  firstName: "Kyle",
  lastName: "Cook",
  printName() {
    console.log(`${this.firstName}${this.lastName}`)
  },
}

person.printName()
```

<details>
<summary>Solution</summary>

```js
Kyle Cook
```

</details>
