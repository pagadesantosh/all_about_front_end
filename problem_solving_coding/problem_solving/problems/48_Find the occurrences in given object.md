## Find the occurrences

```js
function countGender(people) {
  const genderCount = {};

  for (let person of people) {
    if (!genderCount[person.gender]) {
      genderCount[person.gender] = 1; // If the gender hasn't been counted yet, initialize it with 1
    } else {
      genderCount[person.gender]++; // Otherwise, increment the count
    }
  }

  return genderCount;
}

const people = [
  { name: 'Mary', gender: 'girl' },
  { name: 'Paul', gender: 'boy' },
  { name: 'John', gender: 'boy' },
  { name: 'Lisa', gender: 'girl' },
  { name: 'Bill', gender: 'boy' },
  { name: 'Maklatura', gender: 'girl' },
  { name: 'Sara', gender: 'girl' },
];

const output = countGender(people);
console.log('boys:', output.boy); // Outputs: "boys: 3"
```
