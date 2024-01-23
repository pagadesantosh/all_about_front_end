## Most Frequently occurring character in a string

**Approach Taken**

1. maintain an obj, maxCount variable (number), and a result array
2. for of loop on stringParam to get each and every character
3. check this character inside the obj.. Ex: `obj[eachAndEveryChar] = (obj[eachAndEveryChar]||0)+ 1`
4. similarly maxCount is mutated (ex: maxCount = Math.max(maxCount, obj[eachAndEveryChar])) ----> Math.max(0, 1) for the very first time
5. 2nd loop: for in loop (this loop is for iterating keys inside the object )
6. if(obj[eachAndEveryChar] === maxCount) push this inside result array
7. core logic: sometimes result will have c and e as maxCharacters, sometimes one char is max (that is why we are checking the `return result.length === 1 ? result[0]: result`)

```js
function mostRepeatedChar(inputStr) {
  let charCount = {};
  let maxCount = 0;
  let result = [];

  for (let char of inputStr) {
    charCount[char] = (charCount[char] || 0) + 1; // ex: {a: 1, b: 1, c: 1, d: 1, e: 3}
    if (charCount[char] > maxCount) {
      maxCount = charCount[char];
      result = [char];
    } else if (charCount[char] === maxCount) {
      result.push(char);
    }
  }

  return result.length === 1 ? result[0] : result;
}

console.log('most repeated char count', mostRepeatedChar('abcdeee')); // most repeated char count e
console.log('most repeated char count', mostRepeatedChar('abcccdeee')); // most repeated char count ['c', 'e']
```
