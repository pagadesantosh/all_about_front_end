##### HTML page:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="script.js" defer></script>
  </head>
  <body></body>
</html>
```

---

#### append

- With append, you can append anything (including elements)

```js
// script.js
const body = document.body
body.append("Hello World")
```

<img width="227" alt="image" src="https://user-images.githubusercontent.com/42731246/214130886-17caad7c-21a7-40cc-b082-4c53a95f0fd9.png">

---

##### appendChild

- With appendChild, you can only append elements like div, span

```js
const body = document.body
body.appendChild("Hello World")
```

## <img width="329" alt="image" src="https://user-images.githubusercontent.com/42731246/214230120-83c4f6ab-3add-49f3-8249-325a56e2cacd.png">

---

##### Creating a div element and append to body

- In script.js file

```js
// script.js
const body = document.body
const div = document.createElement()
body.append(div)
```

<img width="320" alt="image" src="https://user-images.githubusercontent.com/42731246/214230783-a266ce90-c2cb-4049-a63e-cea693b8333b.png">

---

##### Adding text to a div element

```js
// script.js
const body = document.body
const div = document.createElement()
div.innerText = "Hello World"
// div.textContent = "Hello World"; (can be also used)
body.append(div)
```

<img width="538" alt="image" src="https://user-images.githubusercontent.com/42731246/214231001-09f98f6b-af3d-49ba-8b28-357887eb63b9.png">

<img width="203" alt="image" src="https://user-images.githubusercontent.com/42731246/214231074-2c3992a4-d7f9-4783-a836-9258b5dd857b.png">

---

#### innerText vs textContent

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="script.js" defer></script>
  </head>
  <body>
    <div>
      <span>Hello</span>
      <span style="display:none">Bye</span>
    </div>
  </body>
</html>
```

```js
const div = document.querySelector("div")
console.log(div.textContent) // prints everything like indentation
console.log(div.innerText) // just prints out the text

// innerText doesn't print the text if it is not visible
```

<img width="321" alt="image" src="https://user-images.githubusercontent.com/42731246/214346745-dc3d2e90-2d70-4abd-9b55-dd5453aacf5b.png">

---

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="script.js" defer></script>
  </head>
  <body>
    <div>
      <span id="hi">Hello</span>
      <span id="bye">Bye</span>
    </div>
  </body>
</html>
```

```js
//script.js
const body = document.body
const div = document.querySelector("div")
const spanHi = document.queerySelector("#hi")
const spanBye = document.queerySelector("#bye")

spanBye.remove() // removes the element
```

<img width="326" alt="image" src="https://user-images.githubusercontent.com/42731246/214354436-4758d513-b3bb-4f54-a4cd-ff986f3ad9d8.png">

---

#### Another Example (adding title attribute):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="script.js" defer></script>
  </head>
  <body>
    <div>
      <span title="hello" id="hi">Hello</span>
      <span id="bye">Bye</span>
    </div>
  </body>
</html>
```

```js
//script.js
const body = document.body
const div = document.querySelector("div")
const spanHi = document.querySelector("#hi")
const spanBye = document.querySelector("#bye")

console.log(spanHi.getAttribute("id")) // prints out the id which is "hi"
console.log(spanHi.getAttribute("title")) // prints out the tile which is "hello"

// We can also use below instead of getAttribute()
console.log(spanHi.id)
console.log(spanHi.title)

// Similary we can setAttribute
spanHi.setAttribute("id", "sdfsdfsd")

// We can also use below instead of setAttribute()
spanHi.id = "sdfsdfsd"
```

<img width="319" alt="image" src="https://user-images.githubusercontent.com/42731246/214356059-01242fb7-31a1-4545-8d8d-6af8f7ca8eda.png">

##### removeAttribute

<img width="814" alt="image" src="https://user-images.githubusercontent.com/42731246/214356274-e5daadb1-ffd9-4d38-9706-313c1eba79c1.png">

---

#### Another Example (adding data-test attribute):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="script.js" defer></script>
  </head>
  <body>
    <div>
      <span title="hello" id="hi" data-test="this is a test">Hello</span>
      <span id="bye">Bye</span>
    </div>
  </body>
</html>
```

```js
//script.js
const body = document.body
const div = document.querySelector("div")
const spanHi = document.querySelector("#hi")
const spanBye = document.querySelector("#bye")

console.log(spanHi.dataset)
```

## <img width="323" alt="image" src="https://user-images.githubusercontent.com/42731246/214366534-be277f62-9ffa-4d81-ad80-9a1ee3455cdf.png">

---

#### Another Example (adding data-longer-name attribute):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="script.js" defer></script>
  </head>
  <body>
    <div>
      <span
        title="hello"
        id="hi"
        data-test="this is a test"
        data-longer-name="sdsdfsd"
        >Hello</span
      >
      <span id="bye">Bye</span>
    </div>
  </body>
</html>
```

```js
//script.js
const body = document.body
const div = document.querySelector("div")
const spanHi = document.querySelector("#hi")
const spanBye = document.querySelector("#bye")

console.log(spanHi.dataset)
console.log(spanHi.dataset.longerName) // you can access from the DOM
spanHi.dataset.longerName = "hi" // you can modify
```

<img width="420" alt="image" src="https://user-images.githubusercontent.com/-42731246/214367068-48066c13-088b-4ab5-b365-7d3eaa40b1c4.png">

---

#### Another Example (adding class attribute):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script src="script.js" defer></script>
  </head>
  <body>
    <div>
      <span title="hello" id="hi" class="hi1 hi2">Hello</span>
      <span id="bye">Bye</span>
    </div>
  </body>
</html>
```

```js
//script.js
const body = document.body
const div = document.querySelector("div")
const spanHi = document.querySelector("#hi")
const spanBye = document.querySelector("#bye")

spanHi.classList.add("new-class") //add
spanHi.classList.remove("hi1") //remove

// removes hi2 if it is there, otherwise it adds hi2
spanHi.classList.toggle("hi2") //toggle

// automatically removes if false is passed
spanHi.classList.toggle("hi2", false) //toggle

// automatically add the class if true is passed
spanHi.classList.toggle("hi2", true) //toggle
```

<img width="809" alt="image" src="https://user-images.githubusercontent.com/42731246/214368776-5d997c75-c8cd-41ce-a243-b254a9a5efd7.png">

---
