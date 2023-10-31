#### Pure Functions are those functions that are deterministic in nature

<i>If you gonna pass same set of arguments, you would be expecting same set of outputs</i>

```js
function areaOfRectangle(length, width) {
  return length * width
}
console.log(areaOfRectangle(10, 20))
console.log(areaOfRectangle(10, 20))
```

---

#### Impure Function

<i>Same set of arguments are passed but we are not going to get same set of outputs</i>

```js
function test(length, width) {
  const temp = Math.floor(Math.random() * 10)
  return length * width * temp
}

console.log(test(10, 20))
console.log(test(10, 20))
```

<i>Real time scenario for Impure Function is a function that is calling a api (which is indeterministic)</i>

---

#### Question 1:

```js
let output = console.log("Hello World")
console.log("Output is" + output)
```

<details>
<summary>Solution</summary>

```js
- console.log is a function
- console.log as a function always returns undefined
- As it always returning undefined, it is a deterministic function (always returns same value)
- That is why console.log is a pure function
```

</details>

---

#### Question 2:

```js
function areaOfRectangle(length, breadth) {
  console.log(" Area is " + length * breadth)
  return length * breadth
}
areaOfRectangle(2, 4)
```

<details>
<summary>Solution</summary>

```js
- console.log is a function
- Adding console.log makes a function Impure (Side Effect)
- As it always returning undefined, it is a deterministic function (always returns same value)
- That is why console.log is a pure function
```

</details>

---

#### Question 3: (Array.filter method is pure or not)

```js
const words = ["spray", "destruction"]
const result = words.filter((word) => word.length > 6)
console.log(result)
```

<details>
<summary>Solution</summary>

```js
- pure function
- Since words.filter is not enclosed in any function (words.filter) is pure function.
```

</details>

---

#### Question 4:

```js
function uncommonGeek() {
  const words = ["spray", "destruction"]
  const result = words.filter((word) => word.length > 6)
  console.log(result) // Output will be ['destruction']
}
```

<details>
<summary>Solution</summary>

```js
- uncommonGeek is not a pure function
- Since words.filter is not enclosed in any function (words.filter) is pure function.
```

</details>

---

#### Question 5 : Why pure functions are essential

<details>
<summary>Solution</summary>

1. Deterministic
2. Memoization

```js
- Due to they are deterministic in nature they are very useful in the long run.
- As they are not going to change the outputs, it can be used at multiple places in your project.
- When we are calling something we will be checking if that value already exists in the memory or not

Ex: if we know that same values are passed everytime, then we rather store them instead of computing
```

</details>
