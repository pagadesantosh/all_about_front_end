##### Closure is "when you have a function defined inside of another function, that inner function has access to the variables and scope of the outer function even if the outer function finishes executing and those variables are no longer accessible outside of that function."

```js
function outerFunction(outerVariable) {
  return function innerFunction(innerVaraible) {
    console.log("Outer Variable:" + outerVariable);
    console.log("Inner Variable:" + innerVariable);
  };
}

const newFunction = outerFunction("outside");
newFunction("inside");

// Output:
Outer Variable: outside
Inner Variable: inner
```

<strong>Code Walkthrough</strong>:

- When we first call the outerFunction, we have this outerVariable which we set to 'outside'
- The reason why we're able to access the outerVariable inside the of innerFunction is because of the Closures.
- When the outerFunction runs, the outerVariable is only available inside the outerFunction (but this function is done executing)

```js
//This line executes all the innerFunction code
const newFunction = outerFunction("outside")
console.log(outerVariable) // Reference Error: 'outerVariable' is not defined
```

- This is where Closures come into picture
- As innerFunction is inside the outerFunction it has this outerVariable access and <strong>it saves this outerVariable even if the function that defined this variable is no longer executed anymore or it exits out of the function</strong>. It's still gonna to keep track of the outer variable
