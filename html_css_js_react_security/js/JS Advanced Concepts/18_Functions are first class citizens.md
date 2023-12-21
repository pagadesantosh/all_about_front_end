### 18. Functions are first class citizens:

**_1. Functions can be assigned to variables and properties of objects_**

```js
//1
var func = function () {};
```

**_2. We can also pass functions as arguments into a function._**

```js
//2
function a(fn) {
  fn();
}

a(function () {
  console.log('hi');
});
```

**_3. You can return functions as values from other functions_**

```js
//3
function b() {
  return function c() {
    console.log('bye');
  };
}

var d = b();
d();
```
