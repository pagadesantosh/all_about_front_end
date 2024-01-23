### Find the Index of the First Occurrence in a String

- take the length of both of the params
- basic for loop with logic of i<= firstParamLength - secondParamLength
- core logic is : if(param1.substring(forLoopIndex, forLoopIndex + param2.length) === "param2Itself") then return the forLoopIndex
- return -1 (on outside the for loop)

```js
function strStr(haystack, needle) {
  if (needle === '') return 0; // Edge case: empty needle

  const n = haystack.length; //ex: "sadbutsad".length is 9
  const m = needle.length; //ex: "sad".length is 3

  for (let i = 0; i <= n - m; i++) {
    //"sadbutsad".substring(0, 0+3) === "sad"
    if (haystack.substring(i, i + m) === needle) {
      return i; // Found the needle
    }
  }

  return -1; // Needle not found
}

// Example usage
console.log(strStr('sadbutsad', 'sad')); // Output: 0
console.log(strStr('leetcode', 'leeto')); // Output: -1
```
