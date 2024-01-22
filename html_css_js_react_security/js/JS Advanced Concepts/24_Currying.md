### Currying

- is the technique of **_translating the evaluation of a function_** that takes **_multiple arguments_** into evaluating a **_sequence of functions each with a single argument_**.

**Example**

```js
// Normal Func
const multiply = (a, b) => a * b;
multiply(3, 4); //12
```

```js
const multiply = (a) => (b) => a * b;
// Example Invocation: 1
multiply(3)(4); //12

// Example Invocation: 2
const multiplyBy5 = multiply(5);
console.log(multiplyBy5(4)); // 20
```

---

### Partial Application

- Partially apply a function
- Process of producing a function with a smaller number of parameters
- Means, taking a function, applying some of its arguments into the function (remembers those parameters) and then it uses closures to later on be called with all the rest of the arguments.

Ex: Instead of taking 3 or more arguments, we are giving one param once, and rest of the params for the 2nd invocation. (Call the function once and apply the rest of the arguments to it. For the 2nd call I expect all the arguments)

```js
//curried function
const curriedFunc = (a) => (b) => (c) => a * b * c;
curriedFunc(3)(4)(5); //60
```

```js
//partial function
const normalFunc = (a, b, c) => a * b * c;
const partialMultiplyBy5 = normalFunc.bind(null, 5); // 5 applied to a, null is this context (which we don't care here)
partialMultiplyBy5(4, 10); // 40*5 is 200
```

<u>***Summary***</u>:
- Currying means I expect argument at a time.
- Partial means I expect all the arguments at second call.