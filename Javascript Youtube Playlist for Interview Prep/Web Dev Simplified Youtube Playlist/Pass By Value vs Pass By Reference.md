### Pass By Value

- ##### Primitive Types like Number, Boolean, String, undefined, null

```js
let x = 10;
let y = "Hi";
let x = true;
```

##### After assigning 'c' variable equal to 'a' (let c = a), even if we change the 'c' value it doesn't effect the 'a' value because values are pointed out to separate memory location here.

<img width="444" alt="image" src="https://user-images.githubusercontent.com/42731246/213954104-84a450de-c04d-4598-b489-50ce36264d1d.png">

---

### Pass By Reference:

- Arrays, Objects, Classes are passed by reference and thus can be modified.

- variable c is an array and it points out to the memory address
- After assigning 'd' variable equal to 'c' (let d = c), it doesn't create a new memory location for variable 'd' (instead points out to the same memory address/location)
- after assigning (let d = c), if we are performing any operation on one of the variable (c or d), then it changes the values of both (variable c and d)

##### Below is the example:

- variable c and variable d now prints [1,2,3] if logged because they are pointing to same memory location.

<img width="571" alt="image" src="https://user-images.githubusercontent.com/42731246/213954630-910fa1bb-4eda-405e-8293-63fd3e342a24.png">

---

#### Example 2 (Pass By Reference)

- If we are assigning a new array to 'd' variable, it points out to new memory location
- So now if we update 'd' or 'c' they are independent to each other (doesn't change values of either 'c' if 'd' is updated or vice-versa)

<img width="572" alt="image" src="https://user-images.githubusercontent.com/42731246/213955334-c082f623-6576-46d5-9d5f-07604335d130.png">

---

#### Few Examples

```js
let a = 10;
let b = "Hi";
let c = a;

console.log(`a = ${a}`);
console.log(`b = ${b}`);
console.log(`c = ${c}`);
```

<details>
<summary>Solution</summary>
 a = 10

b = Hi
c = 10

</details>

---

```js
let a = 10;
let b = "Hi";
let c = a;
c = c + 1; // incrementing by 1

console.log(`a = ${a}`);
console.log(`b = ${b}`);
console.log(`c = ${c}`);
```

<details>
<summary>Solution</summary>
 a = 10

b = Hi
c = 11

</details>

---

```js
let a = 10;
let b = "Hi";
let c = [1, 2]; // array
let d = c; // making both equal
d.push(3);

console.log(`a = ${a}`);
console.log(`b = ${b}`);
console.log(`c = ${c}`);
console.log(`d = ${d}`);
```

<details>
<summary>Solution</summary>
 a = 10

b = Hi
c = 1,2,3
d = 1,2,3

</details>

---

```js
let a = 10;
let b = "Hi";
let c = [1, 2]; // new array
let d = [3, 4, 5]; // assigning new array
d.push(6);

console.log(`a = ${a}`);
console.log(`b = ${b}`);
console.log(`c = ${c}`);
console.log(`d = ${d}`);
```

<details>
<summary>Solution</summary>
 a = 10

b = Hi
c = 1,2
d = 3,4,5,6

</details>

---

```js
let c = [1, 2]; // new array
let d = c;

console.log(`c === d ${c === d}`);
console.log(`c == d ${c == d}`);
```

<details>
<summary>Solution</summary>
c === d true

c == d true

<strong>Reason:</strong> Both are pointing to same memory address

Ex:

```js
let c = [1, 2]; // 0x01
let d = c; // 0x01
```

</details>

---

```js
let c = [1, 2]; // new array
let d = [1, 2]; // new array

console.log(`c === d ${c === d}`);
console.log(`c == d ${c == d}`);
```

<details>
<summary>Solution</summary>
c === d false

c == d false

<strong>Reason:</strong> Both are pointing to different address

Ex:

```js
let c = [1, 2]; // 0x01
let c = [1, 2]; // 0x02
```

<strong>Note:</strong> Even though values are same in this case, as we are creating in a <strong>separate line, it takes new memory address</strong>

</details>

---

```js
let c = [1, 2]; // 0x01
console.log(`c = ${c}`);
add(c, 3);
console.log(`c = ${c}`);

function add(array, element) {
  array.push(element);
}
```

<details>
<summary>Solution</summary>
c = 1,2

c = 1,2,3

<strong>Reason:</strong> before invoking the function one console.log is printed and after invoking the function 'c' variable has performed the push operation (so it holds the '3' value in the array)

</details>

---

```js
const c = [1, 2]; // 0x01
c.push(3);
console.log(`c = ${c}`);
```

<details>
<summary>Solution</summary>
c = 1,2,3

</details>
