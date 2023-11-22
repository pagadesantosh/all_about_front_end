## Count the number of vowels in a given string

**Approach Taken**

1. Create a variable string containing all the vowels and create a variable string containing all the vowels (Ex: "aeiouAEIOU")
2. one for loop for str.length, another for loop inside the first for loop (2nd for loop is to vowels.length)
3. Core logic is: If the character is a vowel, increment a counter(ex: char[i] === vowel[j]) count++ and break

Here's the code for the above logic:

```javascript
let a = 'saiteja';
let vowels = 'aeiouAEIOU'; // considering both lowercase and uppercase vowels
let count = 0;

for (let i = 0; i < a.length; i++) {
  for (let j = 0; j < vowels.length; j++) {
    if (a[i] === vowels[j]) {
      count++;
      break;
    }
  }
}

console.log(count); // Outputs: 3
```

---

## Another trick question related to vowels

```js
let a = 'saiteja';
let vowels = 'aeiouAEIOU';
let usedVowels = '';

for (let i = 0; i < a.length; i++) {
  for (let j = 0; j < vowels.length; j++) {
    if (a[i] === vowels[j]) {
      // above if condition is true for a,e,i because these three are part of string saiteja
      // Check if the vowel is already identified (ex: ''.indexOf(indexOfaChar) is not present then usedVowels will store that char)
      if (usedVowels.indexOf(a[i]) === -1) {
        usedVowels += a[i];
      }
      break;
    }
  }
}

console.log(usedVowels); // Outputs: "aie"
```

##### Solution 2

```js
let a = 'saiteja';
let vowels = new Set('aeiouAEIOU');
let usedVowels = new Set();

for (let char of a) {
  if (vowels.has(char)) {
    usedVowels.add(char);
  }
}

console.log([...usedVowels].join('')); // Outputs: "aie"
```
