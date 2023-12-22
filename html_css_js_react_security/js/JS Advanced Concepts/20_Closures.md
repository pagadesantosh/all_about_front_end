### 20. Closures

##### We have closures in javascript because of these two things:

- **1. function()**
- **2. Lexical Scope**

<u>**_Closures is simply a combination of function and the lexical scope environment from which it was declared._**</u>

<u><b>Note:</b></u> Closures **_allow a function to access variables_** from an enclosing scope or environment, **_even after it is closed and executed_**.

```js
function a() {
  var grandpa = 'grandpa';
  return function () {
    var father = 'father';
    return function () {
      var son = 'son';
      return `${grandpa} > ${father} > ${son}`;
    };
  };
}
console.log(a()()()); // grandpa > father > son

// a and b are `Higher order functions` because they return functions
// whereas c is a normal function because it returns someValue at the end
```

- **_The beauty of the closure is even after the `function a` is invoked and executed and popped off from the call stack, `function b and function c` can still access `function a` variable_**

- The javascript engine will make sure that the **_function has access to all the variables outside of the function with this closure_**.

- So instead of garbage collected, JS engine sees that these functions formed as a closure and thereby putting them into the closure box after invocation. Instead of c checking the variables in the GOC(Global Execution Context), it checks first in the Closure box and when it finds them in the box, it returns them.

```js
//Example 1
function callFunc() {
  const callMe = 'Hi!';
  setTimeout(function () {
    console.log(callMe); //after 4seconds logs Hi!
  }, 4000);
}

callFunc();
```

```js
//Example 2, by the time setTimeout is back for execution, it has the value of callMe variable
function callFunc() {
  setTimeout(function () {
    console.log(callMe); //after 4seconds logs Hi!
  }, 4000);
  const callMe = 'Hi!';
}

callFunc();
```

#### Closures Advantages

##### 1. Memory Efficient

```js
// Normal Function
function heavyDuty(index) {
  const bigArray = new Array(7000).fill('emoji');
  console.log('Created');
  return bigArray[index];
}

console.log(heavyDuty(688));
console.log(heavyDuty(688));
console.log(heavyDuty(688));

// Output:
Created;
emoji;
Created;
emoji;
Created;
emoji;
```

```js
// With Closures
function heavyDuty2() {
  const bigArray = new Array(7000).fill('emoji');
  console.log('Closures');
  return function (index) {
    return bigArray[index];
  };
}

const getHeavyDuty = heavyDuty2();
console.log(getHeavyDuty(688));
console.log(getHeavyDuty(888));

// Output:
Closures;
emoji;
emoji;
```

##### 2. Data Encapsulation

- by hiding the main logic data and showing only the non-priority ones

```js
function Counter() {
  let count = 0; // Private variable

  //returning only three functions, so we can only access them, thereby making count variable as a hidden variable
  return {
    increment: function () {
      count += 1;
    },
    decrement: function () {
      count -= 1;
    },
    getCount: function () {
      return count;
    },
  };
}

const myCounter = Counter(); // Create a new counter instance

myCounter.increment();
myCounter.increment();
console.log(myCounter.getCount()); // Output: 2

myCounter.decrement();
console.log(myCounter.getCount()); // Output: 1

// Direct access to 'count' variable is not possible
// console.log(myCounter.count); // Undefined
```

#### Examples Code Snippets:

```js
//output only once
let view;
function initialize() {
  let called = 0;
  return function () {
    if (called > 0) {
      return;
    } else {
      view = 'view';
      called++;
      console.log('view has been set')
    }
  };
}
const startOnce = initialize()
startOnce();
startOnce();
startOnce();
console.log(view)

//Output: even though we invoked 3 times, it outputs only once
view has been set
view
```

```js
//using var with setTimeout + IIFE's

const array1 = [1, 2, 3, 4];
for (var i = 0; i < array1.length; i++) {
  (function (index) {
    setTimeout(function () {
      console.log("I'm at index " + array1[index]);
    }, 1000);
  })(i);
}

// Output:
// I'm at index 1
// I'm at index 2
// I'm at index 3
// I'm at index 4
```
