#### Currying is a process in functional programming in which we can transform a function with multiple arguments into a sequence of nesting functions. It returns a new function that expects the next argument inline

#### Question 1 - Write a function that adds up two numbers using add(10)(20)

<details>
<summary>Solution</summary>

```js
function add(x) {
  return function (y) {
    return x + y
  }
}

const output = add(10)(20)
console.log(output)
```

</details>

---

#### Question 2 - Write a function that adds up two numbers using both add(10)(20) and add(10,20)

<details>
<summary>Solution</summary>

```js
function add(x) {
  if (arguments.length > 1) {
    let sum = 0
    for (let i = 0; i < arguments.length; i++) {
      sum += arguments[i]
    }
    return sum
  } else {
    return function (y) {
      return x + y
    }
  }
}

const output = add(10)(20)
const output = add(10, 20)
console.log("With Closure", output)
console.log("Without Closure", output)
```

</details>

---

#### Question 3 - Write a simple currying function that takes infinite number of arguments.

<details>
<summary>Solution</summary>

```js
const sum = (x) => (y) => y ? sum(x + y) : x
console.log(sum(1)(2)(3)(5)(7)())
```

</details>

---
