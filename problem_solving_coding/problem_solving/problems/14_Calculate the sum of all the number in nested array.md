**calculate sum of numbers in an nested array**

**Approach Taken**

1. maintain a sum to keep on adding it inside the for-of loop
2. during for of loop, check if each element is satisfies the Array.isArray(eachElement), if yes then simply mutate the el = recursiveFunction(el)
3. if that condition is not true then outside to that if condition, keep on adding the sum (ex: sum= sum + el, that means 1 + 2)
4. outside the for of loop, return that sum

```js
function sumArray(ar) {
  var sum = 0;
  //el is the 1 at first, then 2 then [3, [4], [5, 6]], and this will be passed recursively and will be moved till 7
  for (var el of ar) {
    if (Array.isArray(el)) {
      el = sumArray(el); //recursion
    }
    //if it is non-array, then simply add to the existing sum (ex: 0+1, 1+2, 3+4 and so on...)
    sum += el;
  }
  //outside the for of loop, return the finalSum
  return sum;
}
console.log(sumArray([1, 2, [3, [4], [5, 6]], [7]])); //28
```
