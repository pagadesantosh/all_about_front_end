1. **Two Sum**: Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

```js
// Example 1
Input: (nums = [2, 7, 11, 15]), (target = 9);
Output: [0, 1];
```

```js
// Example 2
Input: (nums = [3, 2, 4]), (target = 6);
Output: [1, 2];
```

```js
// Example 3
Input: (nums = [3, 3]), (target = 6);
Output: [0, 1];
```

<details>
<summary>View Answer</summary>

</details>

---

**2. Return the majority element repeated in the array**

```js
Example 1:
Input: nums = [3,2,3]
Output: 3

Example 2:
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```

<details>
<summary>View Answer</summary>

</details>

---

**3. Move Zeroes - move all 0's to the end of it while maintaining the relative order of the non-zero elements.**

<b>Note:</b> you must do this in-place without making a copy of the array.

```js
Example 1:
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```

```js
function moveZeroes(nums) {
  let lastNonZeroFoundAt = 0;

  // Move all the non-zero elements to the beginning of the array
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] !== 0) {
      let temp = nums[i];
      nums[i] = nums[lastNonZeroFoundAt];
      nums[lastNonZeroFoundAt] = temp;
      lastNonZeroFoundAt++;
    }
  }
}

// Example usage
const nums = [1, 0, 0, 2, 3];
moveZeroes(nums);
console.log(nums); // [1, 2, 3, 0, 0]
```

---

**4. Max Consecutive Ones - return the max number of consecutive 1's in the array**

```js
Example 1:

Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.
Example 2:

Input: nums = [1,0,1,1,0,1]
Output: 2

```

---

**5. Missing Number in an Array**

<details>
<summary>View Answer</summary>

```js
let missingNumber = function (nums) {
  let sum = 0
  for (let i = 0; i < nums.length; i++) {
    sum += nums[i]
  }
  return (nums.length * (nums.length + 1)) / 2 - sum
}

// One Line Solution:
let missingNumber = (nums) =>
(nums.length \* (nums.length + 1)) / 2 - nums.reduce((acc, num) => num + acc)

console.log(missingNumber([3, 0, 1])) // 2
console.log(missingNumber([9, 6, 4, 2, 3, 5, 7, 0, 1])) // 8

```

</details>

---

**6 Find count of all players**

```js
const data = {
  id: 1,
  name: ['P1', 'P4'],
  next: {
    id: 2,
    name: ['P3'],
    next: {
      id: 3,
      name: ['P3', 'P4', 'P5'],
      next: {
        id: 4,
        name: ['P1', 'P2', 'P4'],
        next: {
          id: 5,
          name: ['P2', 'P3', 'P5'],
          next: null,
        },
      },
    },
  },
};
```

<details>
<summary>View Answer</summary>

```js
const playerCount = (data) => {
  if (data === null) {
    return {};
  }

  let countPlayer = {};
  for (let player of data.name) {
    countPlayer[player] = (countPlayer[player] || 0) + 1;
  }
  const nextPlayerCount = playerCount(data.next);

  for (let key in nextPlayerCount) {
    countPlayer[key] = (countPlayer[key] || 0) + nextPlayerCount[key];
  }
  return countPlayer;
};

const countPlayer = playerCount(data);
console.log(countPlayer); // {p1: 2, p4: 3, p3: 3, p2: 2: p5: 2}
```

</details>

---

**7. Number of Good Pairs**

```js
Example 1:
Input: nums = [1,2,3,1,1,3]
Output: 4
Explanation: There are 4 good pairs (0,3), (0,4), (3,4), (2,5) 0-indexed.

Example 2:
Input: nums = [1,1,1,1]
Output: 6
Explanation: Each pair in the array are good.

Example 3:
Input: nums = [1,2,3]
Output: 0
```

---

**8. Count the Number of Consistent Strings**

```js
Example 1:
Input: allowed = "ab", words = ["ad","bd","aaab","baa","badab"]

Output: 2
Explanation: Strings "aaab" and "baa" are consistent since they only contain characters 'a' and 'b'.

Example 2:
Input: allowed = "abc", words = ["a","b","c","ab","ac","bc","abc"]
Output: 7
Explanation: All strings are consistent.

Example 3:
Input: allowed = "cad", words = ["cc","acd","b","ba","bac","bad","ac","d"]
Output: 4
Explanation: Strings "cc", "acd", "ac", and "d" are consistent.
```

---

**9 Unique Number of Occurrences**

```js
Example 1:
Input: arr = [1,2,2,1,1,3]
Output: true
Explanation: The value 1 has 3 occurrences, 2 has 2 and 3 has 1. No two values have the same number of occurrences.

Example 2:
Input: arr = [1,2]
Output: false

Example 3:
Input: arr = [-3,0,1,-3,1,1,1,-3,10,0]
Output: true
```

---

**10. Longest Substring Without Repeating Characters**

```js
Example 1:
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.


Example 3:
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

---

**11. Find the Index of the First Occurrence in a String**

```js
Example 1:
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.

Example 2:
Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.
```

---

**12. Longest Consecutive Sequence- Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.**

```js
Example 1:
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
Explanation: The longest consecutive elements sequence is [0, 1, 2, 3, 4, 5, 6, 7, 8]. Therefore its length is 9.
```

---

**13.First Unique Character in a String - Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.**

```js
Example 1:
Input: s = "leetcode"
Output: 0

Example 2:
Input: s = "loveleetcode"
Output: 2

Example 3:
Input: s = "aabb"
Output: -1
```

---

**14.Find Common Characters - Given a string array words, return an array of all characters that show up in all strings within the words (including duplicates). You may return the answer in any order.**

```js
Example 1:
Input: words = ["bella","label","roller"]
Output: ["e","l","l"]

Example 2:
Input: words = ["cool","lock","cook"]
Output: ["c","o"]
```

---

**15. Sort Characters By Frequency - sort it in decreasing order based on the frequency of the characters. The frequency of a character is the number of times it appears in the string. Return the sorted string. If there are multiple answers, return any of them.**

```js
Example 1:
Input: s = "tree"
Output: "eert"
Explanation: 'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.

Example 2:
Input: s = "cccaaa"
Output: "aaaccc"
Explanation: Both 'c' and 'a' appear three times, so both "cccaaa" and "aaaccc" are valid answers.
Note that "cacaca" is incorrect, as the same characters must be together.

Example 3:
Input: s = "Aabb"
Output: "bbAa"
Explanation: "bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

---

**16. Reverse Vowels of a String**

```js
Example 1:
Input: s = "hello"
Output: "holle"

Example 2:
Input: s = "leetcode"
Output: "leotcede"
```

---
