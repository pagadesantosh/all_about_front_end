- Placing "use strict" at the top of the file
- If you're using classes, you already using "use strict" mode
- by using type="module" in index.html, it automatically enters into strict mode

![image](https://user-images.githubusercontent.com/42731246/215263581-d5b196bb-4e5f-418b-a12c-b672cb8607b7.png)

#### Example 1

- strict mode doesn't allow us to create acciedental variables.

```js
"use strict"
let variable = "value"
vriable = 10

console.log(variable, window.vriable)
```

![image](https://user-images.githubusercontent.com/42731246/215263728-38e5cba7-b384-4490-9355-261cbdee305d.png)

---

#### Example 2

- strict mode doesn't allow us to assign the read only properties.

```js
"use strict"
undefined = 10
NaN = 10

console.log(window.undefined)
```

![image](https://user-images.githubusercontent.com/42731246/215263795-8ae8b9a4-9ed4-49f7-acc1-841c0067d739.png)

---

#### Example 3

- strict mode doesn't allow us to assign the read only properties.

```js
"use strict"
const obj = {}
Object.defineProperty(obj, "readOnly", { writable: false, value: 10 })
obj.readOnly = 15
console.log(obj)
```

![image](https://user-images.githubusercontent.com/42731246/215263891-0c50d437-f7f1-45e7-93d3-0c2b5f5cce40.png)

---

#### Example 4

- accidental typo in the parameters

```js
"use strict"

function combine(a, a, c) {
  return [a, a, c]
}

console.log(combine(1, 2, 3))
```

![image](https://user-images.githubusercontent.com/42731246/215263999-40c1e4f6-8099-4392-b6b4-ffe2cdb4738b.png)

---

#### Example 5

- Octal Literals
- Without use strict, it prints out 13 on the console.

```js
"use strict"
console.log(015)
```

![image](https://user-images.githubusercontent.com/42731246/215264045-6f3eb7cd-38a6-4d51-a133-d57393e46a44.png)

---

#### Example 6

- Adding prop to Primitives (Number, String, boolean, undefined, null)

```js
"use strict"
const v = "value"
v.prop = 10
console.log(v.prop)
```

![image](https://user-images.githubusercontent.com/42731246/215264182-9c51b93a-0934-4fc9-9592-5f69d7b4c26d.png)

---

#### Example 7 (Without "use strict")

```js
function sum(a, b) {
  console.log(this) // prints Window object
  return a + b
}

console.log(this) // prints Window object
sum(1, 2)
```

---

#### Example 8 (With "use strict")

- Only inside of a function, this value is undefined

```js
"use strict"
function sum(a, b) {
  console.log(this) // prints undefined
  return a + b
}

console.log(this) // prints Window object
sum(1, 2)
```

---

#### Example 9 (With "use strict" using .bind() method)

- This is a good security feature because you don't want to expose the Window object all over the place
- Sometimes you want to prevent certain things from using the window object like Chrome Extensions

```js
"use strict"
function sum(a, b) {
  console.log(this) // prints Window object
  return a + b
}

console.log(this) // prints Window object
sum.bind(this)(1, 2)
```

---

#### Example 10 (in strict mode)

```js
"use strict"
function sum(a, b) {
  a = 10
  return [a + b, arguments[0] + arguments[1]]
}

console.log(sum(1, 2))
```

![image](https://user-images.githubusercontent.com/42731246/215264954-9b53e5ea-2067-4c00-a2a1-9e2ba7c43ac1.png)

---

#### Example 11 (not in strict mode)

```js
function sum(a, b) {
  a = 10
  return [a + b, arguments[0] + arguments[1]]
}

console.log(sum(1, 2))
```

![image](https://user-images.githubusercontent.com/42731246/215264867-bf92a1e4-207d-4a79-a65e-fdd6361f8e86.png)

---
