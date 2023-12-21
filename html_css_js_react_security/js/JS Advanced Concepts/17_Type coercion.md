### 17. Type coercion

<b><u>Definition:</u></b> Converting a certain type to another type

- The operands on the left vs right are of different types, so in this case one of them will be converted into an equivalent value by the JS engine.
- **_Type coercion happens when we have double equal to_** (==), so this simply means compare two values if both are of different type, coerce one into the same type.
- **_Triple equal to in JS means compare two values, but don't try and coerce the values_**.

<u>**_Useful info Link_**</u> 👉: https://dorey.github.io/JavaScript-Equality-Table/

```js
console.log(false == ''); //true
console.log(false == []); //true
console.log(false == {}); //false
console.log('' == 0); //true
console.log('' == []); //true
console.log('' == {}); //false
console.log(0 == []); //true
console.log(0 == {}); //false
console.log(0 == null); //false
```