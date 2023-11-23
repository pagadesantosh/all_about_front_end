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
function count(str) {
  const counts = {};
  let maxCount = 0;
  const result = [];

  // Count each character's occurrences
  for (const char of str) {
    counts[char] = (counts[char] || 0) + 1;
    maxCount = Math.max(maxCount, counts[char]);
  }

  // Find characters with the maximum count
  for (const char in counts) {
    if (counts[char] === maxCount) {
      result.push(char);
    }
  }

  return result.length === 1 ? result[0] : result;
}

console.log('most repeated char count', count('abcdeee')); // most repeated char count e
console.log('most repeated char count', count('abcccdeee')); // most repeated char count ['c', 'e']
```
