
```js
let findPermutations = (string) => {
  if (!string || typeof string !== 'string') {
    return 'Please enter a string';
  } else if (string.length < 2) {
    return string;
  }

  let permutationsArray = [];

  for (let i = 0; i < string.length; i++) {
    let char = string[i];

    if (string.indexOf(char) != i) continue;

    let remainingChars =
      string.slice(0, i) + string.slice(i + 1);

    for (let permutation of findPermutations(remainingChars)) {
      permutationsArray.push(char + permutation);
    }
  }
  return permutationsArray;
};

console.log(findPermutations('aabc'));
```

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/646cbed5-cc1e-49eb-b1ad-9d38527e558f)
