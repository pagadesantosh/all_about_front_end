- Functional Programming is built on pure functions logic.
- Pure Function is something that doesn't have a side effect and it's a fucntion that always returns the exact same thing every time you give it the same inputs so every single time you call this function with same input will always gonna give you the same output.
- A pure function only depends on its inputs

#### Example 1 (Not a Pure Function)

- This function relies on external information, it's affecting the things outside of the function because with the pure function a function is going to take in some inputs and it's only going to operate on those inputs in order to create the output

```js
const array = [1, 2, 3]

function addElementToArray(element) {
  array.push(element)
}
```

#### Example 2 (Not a Pure Function)

- This function has a side effect as it is changing the input here
- With a pure function you never want to change the inputs that you're adding into the element

```js
const array = [1, 2, 3]

function addElementToArray(a, element) {
  a.push(element)
}
```

#### Example 3 (A Pure Function)

```js
const array = [1, 2, 3]

function addElementToArray(a, element) {
  return [...a, element]
}
```

- No matter how many times we call the function, you can see it always going to return exact same thing

![image](https://user-images.githubusercontent.com/42731246/215322085-a5b899ff-1f32-4a25-8fbf-8ccd22ffa1eb.png)

#### Example 4 (Not a Pure Function)

- Even though it is using the same exact inputs it actually returns the different output each time
- With a pure function you never want to change the inputs that you're adding into the element
- So even though we are using only inputs we get and we're not affecting outside of our function since our function actually gives a different result every single time we call it with the same inputs it's no longer a pure function.
- It has to always return the same output every time you give it the same inputs

```js
const array = [1, 2, 3]

function addElementToArray(a, element) {
  return [...a, element, Math.random()]
}
```

![image](https://user-images.githubusercontent.com/42731246/215322247-aa76563f-491a-4d32-b74a-5a6e9d0ee316.png)
