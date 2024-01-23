## Find the largest difference

```js
largestDiff([-1, 2, 3, 10, 9]);
// 11,  obviously Math.abs(-1 - 10) is the largest

largestDiff([]);
// 0

largestDiff([1]);
// 0
```

**Approach Taken**

1. accept the arrayParam
2. Math.max(...arrayParam) for max, same Math.min(...arrayParam) for min
3. return Math.abs(max-min)

```js
function largestDiff(nums) {
  // If the array has 0 or 1 elements, return 0
  if (nums.length <= 1) {
    return 0;
  }

  // Find the max and min values in the array
  let max = Math.max(...nums);
  let min = Math.min(...nums);

  // Return the absolute difference between max and min
  return Math.abs(max - min);
}

// Test cases
console.log(largestDiff([-1, 2, 3, 17, 9])); // 18
console.log(largestDiff([])); // 0
console.log(largestDiff([1])); // 0
```
