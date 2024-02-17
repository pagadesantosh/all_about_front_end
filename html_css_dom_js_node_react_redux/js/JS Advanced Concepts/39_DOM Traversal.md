#### getElementById

- You can only select one element because only one element can have an id.
- Add <strong>id attribute</strong> to div element or any other element in .html file.

  <img width="329" alt="image" src="https://user-images.githubusercontent.com/42731246/214108551-b86aa733-5c8c-4127-9771-95db5157cc2b.png">

- In the javascript file (script.js), you can access that id attribute using following code

```js
const grandParent = document.getElementById("grandparent-id") // this should match the id attribute provided in .html file
grandParent.style.backgroundColor = "#333"
```

##### Same code in terms of re-usability

```js
const grandParent = document.getElementById("grandparent-id")

changeColor(grandParent)

function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

---

#### getElementsByClassName

- Since multiple elements can have classNames, it always returns a collection of elements (in our case two parent elements)

##### In .html file

<img width="329" alt="image" src="https://user-images.githubusercontent.com/42731246/214111343-6b647ccd-ff7e-4f51-ba6d-092f2d5237e9.png">

##### In .js file

```js
const parents = Array.from(document.getElementsByClassName("parent"))
parents.forEach(changeColor) // changes the backgroundColor for both of the parent classes

function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

---

#### QuerySelector

- To select a single element
- Uses <strong>#</strong> for id
- Uses <strong>.</strong> for class

#### Example for id traversal

```js
const grandParent = document.querySelector("#grandparent-id")
changeColor(grandParent)

function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

#### Example for class traversal

<img width="367" alt="image" src="https://user-images.githubusercontent.com/42731246/214112684-befbb7b6-605f-4fa8-bd0a-576f5349e0d6.png">

```js
const grandParent = document.querySelector(".grandparent")
changeColor(grandParent)

function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

##### In above case we only have one grandparent class (so it worked fine), what if we have two classNames with same naming (ex: below )

## <img width="329" alt="image" src="https://user-images.githubusercontent.com/42731246/214111343-6b647ccd-ff7e-4f51-ba6d-092f2d5237e9.png">

##### Below code only changeColor for 1st parent div

```js
const parent = document.querySelector(".parent")
changeColor(parent)

function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

<img width="412" alt="image" src="https://user-images.githubusercontent.com/42731246/214113936-19608cb1-fb97-435b-89b5-4beca26e65a3.png">

---

#### querySelectorAll

- ##### To Solve the above problem we faced when two div elements have same classNames, we need to use this querySelectorAll

```js
const parents = document.querySelectorAll(".parent")
parents.forEach(changeColor)

function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

   <img width="326" alt="image" src="https://user-images.githubusercontent.com/42731246/214114635-c18b7ca9-782a-436e-b49a-ca623a1c6796.png">

---

#### Selecting Children

- grandparent is the parent class in our case
- two parent classes are the child classes in our case

```js
const grandParent = document.querySelector(".grandparent")
const parents = Array.from(grandParent.children) // To get the children classes

parents.forEach(changeColor)

function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

## <img width="329" alt="image" src="https://user-images.githubusercontent.com/42731246/214111343-6b647ccd-ff7e-4f51-ba6d-092f2d5237e9.png">

##### Let's say if we want to select the specific children (ex: first item)

```js
const grandParent = document.querySelector(".grandparent")
const parents = Array.from(grandParent.children)
const parentOne = parents[0]
const children = parentOne.children

changeColor(children[0])
function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

<img width="348" alt="image" src="https://user-images.githubusercontent.com/42731246/214116397-977708c3-b6f7-4fbb-8ba4-211b579fa66f.png">

---

#### Selecting Descendants

<img width="427" alt="image" src="https://user-images.githubusercontent.com/42731246/214121662-ff0b4fc5-d81a-4105-9565-8ffcde434c56.png">

```js
const grandParent = document.querySelector(".grandparent")
const children = grandParent.querySelectorAll(".child")

children.forEach(changeColor)

function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

<img width="319" alt="image" src="https://user-images.githubusercontent.com/42731246/214121934-15e60c2f-a1ef-4142-8e7d-5f23dd237005.png">

---

#### Selecting Parents

<img width="388" alt="image" src="https://user-images.githubusercontent.com/42731246/214122157-2f487eba-628a-4d8c-8050-0d8f584ae9dc.png">

```js
const childOne = document.querySelector("#child-one")
const parent = childOne.parentElement

changeColor(parent) // parent-div
function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

## <img width="322" alt="image" src="https://user-images.githubusercontent.com/42731246/214122675-5a73ad87-3ee2-4c19-8086-485b8407cfac.png">

##### Example 2:

```js
const childOne = document.querySelector("#child-one")
const parent = childOne.parentElement
const grandParent = parent.parentElement

changeColor(grandParent) // grandParent-div
function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

## <img width="320" alt="image" src="https://user-images.githubusercontent.com/42731246/214123101-b0dca839-e1e3-41ea-a18a-e24f9480d77c.png">

---

#### Selecting Ancestors

- closest works from child to parent traversal
- We took the above code into consideration and removed the parent traversal.
- Output is same for above Example-2 and for this

##### The way how closest works (it looks from child to parent)

<img width="367" alt="image" src="https://user-images.githubusercontent.com/42731246/214124030-2dccc450-a694-4bd2-b1d0-9043b09810da.png">

```js
const childOne = document.querySelector("#child-one")
const grandParent = childOne.closest(".grandparent")

changeColor(grandParent) // grandParent-div
function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

## <img width="320" alt="image" src="https://user-images.githubusercontent.com/42731246/214123101-b0dca839-e1e3-41ea-a18a-e24f9480d77c.png">

---

#### nextElementSibling

- This is something like selecting the second box in our case

```js
const childOne = document.querySelector("#child-one")
const childTwo = childOne.nextElementSibling

changeColor(childTwo)
function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

<img width="323" alt="image" src="https://user-images.githubusercontent.com/42731246/214124606-e74dd500-0442-45f2-950f-77f866136242.png">

---

#### previousElementSibling

- This is something like selecting the first box after been into second box

```js
const childOne = document.querySelector("#child-one")
const childTwo = childOne.nextElementSibling

changeColor(childTwo.previousElementSibling)
function changeColor(element) {
  element.style.backgroundColor = "#333"
}
```

<img width="351" alt="image" src="https://user-images.githubusercontent.com/42731246/214125233-470bdf9a-1904-4cc1-af46-4a1550d41b29.png">
