## Shuffle the array

#### Simple Solution, which returns only one of the shuffled array

```js
function shuffle(arr) {
  for (let i = arr.length - 1; i > 0; i--) {
    const randIdx = Math.floor(Math.random() * (i + 1));
    const storedItem = arr[i];
    arr[i] = arr[randIdx];
    arr[randIdx] = storedItem;
  }

  return arr;
}

// Example usage:
const myArray = [1, 2, 3, 4];
console.log('shuffle', shuffle(myArray));
```

---

#### Simple Solution, which returns all the permutations of shuffled array

```js
function generatePermutations(arr, n = arr.length, result = [], current = []) {
  //if the maintained current array length is same as the passedArgArray length then store it into resultArray (ex: result.push([...current]))
  if (current.length === n) {
    result.push([...current]);
    return;
  }

  for (let i = 0; i < arr.length; i++) {
    if (!current.includes(arr[i])) {
      current.push(arr[i]);
      //recursively calling the function
      generatePermutations(arr, n, result, current);
      current.pop();
    }
  }

  return result;
}

// Example usage:
const myArray = [1, 2, 3, 4];
const permutations = generatePermutations(myArray);

console.log('All possible permutations:');
permutations.forEach((perm) => console.log(perm));
```
