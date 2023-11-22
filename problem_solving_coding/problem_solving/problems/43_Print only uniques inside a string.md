## Print only unique values inside a string

**Approach Taken**

1. Put a for loop for the given input string
2. Put another for loop for `result` string
3. core logic is `isDuplicate = true` and break if inputStr[i] === result[j]
4. Outside to 2nd for loop, inside the first for loop (write the if condition to check the below condition)
5. If it is not duplicate then result = result + inputStr[i]

```js
let inputString = 'saitejaisgoodboy';
let result = '';

for (let i = 0; i < inputString.length; i++) {
  let isDuplicate = false;
  for (let j = 0; j < result.length; j++) {
    if (inputString[i] === result[j]) {
      //core logic is isDuplicate = true
      isDuplicate = true;
      break; //j again starts from 0
    }
  }
  // we want the result string without duplicates, so if that particular character is not duplicate, then result = result + str[i]
  if (!isDuplicate) {
    result += inputString[i];
  }
}

console.log(result); // Outputs: "saitejgodby"
```

---

##### Solution 2: Using Set (O(n))

- The Set-based solution is the most performant with a time complexity of O(n).

```js
let a = 'saitejaisgoodboy';
let result = [...new Set(a)].join('');
console.log(result); // Outputs: "saitejgodby"
```

---

##### Solution 3: Using indexOf (O(n2))

- The outer loop runs n times. The indexOf method has a linear search which in the worst case is O(n). Hence, this method can also be O(n^2) in the worst case.

```js
let a = 'saitejaisgoodboy';
let result = '';

for (let i = 0; i < a.length; i++) {
  if (result.indexOf(a[i]) === -1) {
    result += a[i];
  }
}

console.log(result); // Outputs: "saitejgodby"
```

---

##### Solution 4: Using reduce (O(n2))

- The reduce function runs the callback for each element in the array, which is n times. The includes method also takes O(n) time in the worst case. Thus, this method is O(n^2) in the worst case.

```js
let a = 'saitejaisgoodboy';
let result = a.split('').reduce((acc, curr) => {
  if (!acc.includes(curr)) {
    acc += curr;
  }
  return acc;
}, '');

console.log(result); // Outputs: "saitejgodby"
```

---
