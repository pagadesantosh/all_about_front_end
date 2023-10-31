#### Lexical Scope

- Lexical Scope defines how variable names are resolved in nested functions.
- So if we have a child function inside a parent function then the child function will have access to the variables defined in the parent function and also has access to the global scope
- This is often confused with the closure, Lexical Scope is just a important part of the Closure.

##### Example 1 (Lexical Scope)

```js
//global scope
let x = 1

const parentFunction = () => {
  // local scope
  let myValue = 2
  console.log(x) //1
  console.log(myValue) //2

  const childFunction = () => {
    console.log((x += 5)) //6
    console.log((myValue += 1)) //3
  }
  childFunction()
}

parentFunction()
```

---

#### Closure:

- A closure is a function having access to the parent scope, even after the parent function is closed.

- <strong>Another Definition:</strong> A closure is created when we define a function, not when a function is executed.

##### Example 2 (Closure)

- Although the parent function has already returned and it is already closed but the child function still has access to the scope
- That makes the myValue variable a private variable
- If I log the result() for more than once then it will increment the values

```js
//global scope
let x = 1

const parentFunction = () => {
  // local scope
  let myValue = 2
  console.log(x) //1
  console.log(myValue) //2

  const childFunction = () => {
    console.log((x += 5)) //6
    console.log((myValue += 1)) //3
  }
  return childFunction
}

const result = parentFunction() // calls only parent function and it is closed here
console.log(result) // logs the entire the innner function
result() // returns child function
```

---

##### Example 3 (Closures with IIFE)

- IIFE (Immediately Invoked Function Expression)
- If you don't invoke the privateCounter then it only logs as initial value : 0 (because it is immediately invoked function expression)
- If you log the privateCounter() then it will start printing the inner funciton

```js
const privateCounter = (() => {
  let count = 0
  console.log(`intial value : ${count}`)
  return () => {
    count += 1
    console.log(count)
  }
})()

privateCounter()
```

---

##### Example 3 (Closures with IIFE)

- As it is IIFE it directly logs out the initial credits (without invoking credits() function)
- as you keep on invoking credits() function, it will start decrementing the credits

```js
  cont credits = ((num)=>{
  let credits = num;
  console.log(`inital credits value: ${credits}`)
  return ()=>{
    credits-=1;
    if(credits > 0 ){
      console.log(`playing game, ${credits} credits remaining`)
    }
    if(credits <=0){
      console.log('not enough credits')
    }
  }})(3)

  credits()

```
