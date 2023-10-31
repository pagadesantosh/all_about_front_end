- This conversion between different types is called Implicit type coercion
- The types of our values are being converted without us explicitly telling the type to convert.
- The other type of Type coercion is called explicit type coercion (when we're explicitly converting one type to another).
- parseInt is example of explicit type coercion (because we are explicitly saying that the value we pass has to be converted to a Integer for us). We are purposely telling the code to do it
- Wherease implicit type coercion such as we're taking this numberOfChildren variable (which we don't really know what type it can hold) but at the end we are converting into boolean

#### Can be refereed to as bad code :) :D

```js
const form = document.querySelector("form")
const input = document.querySelector("input")
const errorMsg = document.querySelector(".error")
const successMsg = document.querySelector(".success")

form.addEventListener("submit", (e) => {
  e.preventDefault()
  const numberOfChildren = parseInt(input.value)

  errorMsg.textContent = ""
  successMsg.textContent = ""

  // if numberOfChildren is boolean, following condition check is good approach
  if (!numberOfChildren) {
    errorMsg.textContent = "Please enter number of children"
  } else {
    successMsg.textContent = "Success"
  }
})
```

#### Example 1

- This is going to do an Implicit type coercion where it converts one of these values to the same type of the other to compare them to see if they're equal to each other.

```js
numberOfChildren == false
```

#### Example 2

- This immediately returns false (it doesn't do any implicit type coercion)

```js
numberOfChildren === false
```

#### Can be refereed to as good code

```js
const form = document.querySelector("form")
const input = document.querySelector("input")
const errorMsg = document.querySelector(".error")
const successMsg = document.querySelector(".success")

form.addEventListener("submit", (e) => {
  e.preventDefault()
  const numberOfChildren = parseInt(input.value)

  errorMsg.textContent = ""
  successMsg.textContent = ""

  // if numberOfChildren is boolean, following condition check is good approach
  if (numberOfChildren == null && isNaN(numberOfChildren)) {
    errorMsg.textContent = "Please enter number of children"
  } else {
    successMsg.textContent = "Success"
  }
})
```
