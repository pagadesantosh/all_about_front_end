#### Counter dilemma using Closures

```js
function test() {
  let count = 0
  function add() {
    count = count + 1
    return count
  }
  return add
}

const output = test()
console.log(output())
console.log(output())
console.log(output())
```

<details>
<summary>Solution</summary>

1
2
3

</details>

---

### Question 1: This is not a closure (lexical scope concept)

```js
function init() {
  var name = "Uncommon Geeks"
  function displayName() {
    alert(name)
  }
  displayName()
}
init()
```

<details>
<summary>Solution</summary>

Uncommon Geeks

</details>

---

### Question 2: Using Closure

```js
function makeFunc() {
  var name = "Uncommon Geeks"
  function displayName() {
    alert(name)
  }
  return displayName
}

var myFunc = makeFunc()
```

<details>
<summary>Solution</summary>

Uncommon Geeks

</details>

---

### Question 3:

```js
function makeAdder(x) {
  return function (y) {
    return x + y
  }
}
var add5 = makeAdder(5)
var add10 = makeAdder(10)
console.log(add5(2))
console.log(add10(2))
```

<details>
<summary>Solution</summary>

7
12

</details>

---

### Question 4:

```js
;(function testA(a) {
  return (function testB(b) {
    console.log(a)
  })(1)
})(0)
```

<details>
<summary>Solution</summary>

0

</details>

---

### Question 5:

```js
function test() {
  for (var i = 0; i < 3; i++) {
    setTimeout(function log() {
      console.log(i)
    }, 1000)
  }
}

test()
```

<details>
<summary>Solution</summary>

3
3
3

<strong>Reason:</strong>

- setTimeout formed the closure, and the value of i inside this nested block is bound with the reference of i

- After 1 second, the 3 timers gets expire and it looks for the value of i and at that moment, the value will be 3 (because i is a global scope)

</details>

---

### Question 6:

```js
function test() {
  for (var i = 0; i < 3; i++) {
    setTimeout(function log() {
      console.log(i)
    }, 0) // made 0
  }
}

test()
```

<details>
<summary>Solution</summary>

3
3
3

</details>

---

### Question 7:

```js
function test() {
  for (let i = 0; i < 3; i++) {
    setTimeout(function log() {
      console.log(i)
    }, 0)
  }
}

test()
```

<details>
<summary>Solution</summary>

0
1
2

</details>

---

### Question 8:

```js
function test() {
  for (var i = 0; i < 3; i++) {
    function test1(j) {
      setTimeout(function log() {
        console.log(j)
      }, 1000)
    }
    test1(i)
  }
}

test()
```

<details>
<summary>Solution</summary>

0
1
2

</details>

---
