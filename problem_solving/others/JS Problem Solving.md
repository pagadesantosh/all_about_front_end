1. **Reverse a string** Use `split('')`, `reverse()`, and `join('')`.

<details>
<summary>View Answer</summary>

```js
function reverseString(str) {
  return str.split('').reverse().join('')
}
```

```js
// Example usage:
let original = 'Hello, World!'
let reversed = reverseString(original)
console.log(reversed) // Outputs: "!dlroW ,olleH"
```

</details>

---

2. **Check if a string has all unique characters using only JavaScript methods** Use a set or `indexOf()` and `lastIndexOf()` comparison.

<details>
<summary>View Answer</summary>

- <strong>Approach Taken for Set:</strong>

1. When you apply new Set to the string, it will return the unique characters.
2. So by simply checking the set size with the original string length with `===` results in unique or not.

```js
// Using a Set:
function hasAllUniqueCharsSet(str) {
  return new Set(str).size === str.length
}

// Example:
console.log(hasAllUniqueCharsSet('hello')) // false
console.log(hasAllUniqueCharsSet('abcde')) // true
```

- <strong>Approach Taken for indexOf:</strong>

1. indexOf and lastIndexOf has to be applied on the character (ex: 's')
2. apply a `for of loop` to the str and you will get each and every character
3. str.indexOf(char), str.lastIndexOf(char), if both are not equal return false (ex: "hello" has l at 2 and l at 3)
4. if both are same (ex: string `abcde` has both indexOf and lastIndexOf same), it should exit for loop and return true (so make sure return true is outside of for loop)

```js
// using indexOf and lastIndexOf

function hasAllUniqueCharsIndexOf(str) {
  for (let char of str) {
    if (str.indexOf(char) !== str.lastIndexOf(char)) {
      return false
    }
  }
  return true
}

// Example:
console.log(hasAllUniqueCharsIndexOf('hello')) // false
console.log(hasAllUniqueCharsIndexOf('abcde')) // true
```

</details>

---

3. **Check if two strings are anagrams** Compare sorted versions of both strings.

<details>
<summary>View Answer</summary>

- <strong>Approach Taken for Inbuilt methods :</strong>

1. Accept only a-z, 0-9 and convert the caps into .toLowerCase() (Ex: .toLowerCase().replace)
2. split the string, sort the string and join
3. Function accepts str1, str2 as parameters

```js
function areAnagrams(str1, str2) {
  // Convert to lowercase and remove non-alphanumeric characters
  let cleanStr1 = str1.toLowerCase().replace(/[^a-z0-9]/g, '')
  let cleanStr2 = str2.toLowerCase().replace(/[^a-z0-9]/g, '')

  // Sort and compare
  return (
    cleanStr1.split('').sort().join('') === cleanStr2.split('').sort().join('')
  )
}

// Example usage:
console.log(areAnagrams('listen', 'silent')) // true
console.log(areAnagrams('hello', 'world')) // false
```

- <strong>Approach Taken using for loop :</strong>

1. if the length of the two strings are not same, return false
2. one for loop for str1, one for loop for str2
3. 1st for loop will iterate and calculate each and every character repeated. (ex: s: 1)
4. 2nd for loop will iterate and see if this each and every character is already in the stored object or not
5. Ex: if 'w' character is part of str2 but not in the already stored object then directly return false.
6. if the above condition is false then keep on decrementing the char stored length (ex: 's': 1 to 's': 0)
7. atlast return true saying that passed args are anagrams.

```js
function areAnagrams(str1, str2) {
  if (str1.length !== str2.length) return false

  const charCount = {}

  // Count characters for the first string
  for (let char of str1) {
    charCount[char] = (charCount[char] || 0) + 1
  }

  // Decrease the count based on the second string
  for (let char of str2) {
    if (!charCount[char]) return false // If the character is not in the first string or its count has gone to zero
    charCount[char]--
  }

  return true
}

// Example usage:
console.log(areAnagrams('listen', 'silent')) // true
console.log(areAnagrams('hello', 'world')) // false
```

- **Solution for n number of arguments instead of 2**

- <strong>Approach Taken using for loop :</strong>

1. custom sort for key generation (ex: listen will be sorted to eilnst and will be saved it as a key)
2. a for loop for all the strings, and each and every string will be passed to customSort func
3. if the groups object doesn't has the key groups[key] will be an empty array
4. if it has the key then just push the string (coming as input ex: listen, enlist)
5. if you don't want to see the ouptut as object then simply apply Object.values(your_object)

```js
function customSort(str) {
  let arr = [...str] // Convert string to array

  for (let i = 1; i < arr.length; i++) {
    for (let j = i; j > 0; j--) {
      if (arr[j] < arr[j - 1]) {
        // Swap the characters without using any additional data structure
        ;[arr[j], arr[j - 1]] = [arr[j - 1], arr[j]]
      } else {
        // If the left character is not greater than the right, then break
        break
      }
    }
  }

  return arr.join('') // Convert array back to string
}

function identifyAnagrams(...strings) {
  const groups = {}

  for (let str of strings) {
    const key = customSort(str)
    if (!groups[key]) {
      groups[key] = []
    }
    groups[key].push(str)
  }
  return Object.values(groups)
}

// Example usage:
console.log(
  identifyAnagrams(
    'listen',
    'enlist',
    'slinte',
    'apple',
    'papel',
    'peapl',
    'world',
    'drawer',
    'reward'
  )
)
```

</details>

---

4. **Implement a basic calculator for addition and subtraction without using the `eval` function** Use regular expressions and string methods.

<details>
<summary>View Answer</summary>

- <strong>Approach Taken :</strong>

1. split your numbers
2. match your + and - operators
3. take first number as default
4. if conditon for + and else if condtion for -
5. if true then result = result + successive number
6. else if true then result = result - successive number

```js
function basicCalculator(expression) {
  // Enhanced regex to handle numbers with a leading minus sign correctly
  const numbers = expression.split(/[+-]/).map(Number)
  const operators = expression.match(/[+-]/g) || []

  let result = numbers[0]

  for (let i = 0; i < operators.length; i++) {
    if (operators[i] === '+') {
      result += numbers[i + 1]
    } else if (operators[i] === '-') {
      result -= numbers[i + 1]
    }
  }

  return result
}

console.log(basicCalculator('5+4-3-2')) // 4
console.log(basicCalculator('-5+4-3-2')) // -6
console.log(basicCalculator('5-4-3-2')) // -4
```

</details>

---

5. **Write a function to validate a JSON string** Use try-catch with `JSON.parse()`.

<details>
<summary>View Answer</summary>

- <strong>Approach Taken :</strong>

1. your stringify json object will be passed inside JSON.parse(your_object)

```js
function isValidJSON(jsonString) {
  try {
    JSON.parse(jsonString)
    return true
  } catch (e) {
    return false
  }
}

// Testing the function
console.log(isValidJSON('{"name": "John", "age": 30}')) // true
console.log(isValidJSON('{"name": "John", "age": }')) // false
```

</details>

---

6. **Deep clone an object without using external libraries** Recursion with checking for nested objects and arrays.

<details>
<summary>View Answer</summary>

- <strong>Approach Taken :</strong>

1. An input obj can have an object or null or an array
2. Write three conditions, one for handling objects, arrays, (null and not object)
3. If it is not object (ex: a: 6), then return as it is (i.e the obj passed)
4. If it is array, map with each and every item and pass that item into the function (Which will satisfy one of the three conditions)
5. If it is an object, use a for loop to iterate inside the object and for each property of the source object (obj), it calls the deepClone function recursively

```js
function deepClone(obj) {
  // Handle primitive types and null
  if (obj === null || typeof obj !== 'object') return obj

  // Handle arrays
  if (Array.isArray(obj)) {
    return obj.map((item) => deepClone(item))
  }

  // Handle objects
  const copy = {}
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      copy[key] = deepClone(obj[key])
    }
  }
  return copy
}

// Example usage:
const obj = {
  a: 1,
  b: {
    c: 2,
    d: {
      e: 3,
    },
  },
  f: [4, 5, { g: 6 }],
}

const clonedObj = deepClone(obj)
console.log(clonedObj) // { a: 1, b: { c: 2, d: { e: 3 } }, f: [ 4, 5, { g: 6 } ] }
console.log(clonedObj.b === obj.b) // false, indicating a deep clone
```

</details>

---

7. **Implement throttling or debouncing** Use timeouts and closures.

<details>
<summary>View Answer</summary>

**Throttling**

- A function doesn't get called more often than a specified interval, even it's invoked multiple times.
- Ex: If you throttle a function to be called at most once every 300 ms, it will ignore any additional calls that happen before the 300 ms have passed.

```js
const throttle = (func, limit) => {
  let inThrottle
  return (...args) => {
    if (!inThrottle) {
      func(...args)
      inThrottle = true
      setTimeout(() => (inThrottle = false), limit)
    }
  }
}

// Usage:
const throttledFunction = throttle(() => console.log('Throttled!'), 300)
window.addEventListener('scroll', throttledFunction)
```

**Debouncing**

- A function doesn't get called until after a specified amount of time has passed since it was last invoked.

- Ex: the function won't be called unless 300 ms have passed since the last time it was invoked.

```js
const debounce = (func, delay) => {
  let inDebounce
  return (...args) => {
    clearTimeout(inDebounce)
    inDebounce = setTimeout(() => func(...args), delay)
  }
}

// Usage:
const debouncedFunction = debounce(() => console.log('Debounced!'), 300)
window.addEventListener('resize', debouncedFunction)
```

</details>

---

8. **Flatten a nested array** Recursive approach or using `reduce()`.

<details>
<summary>View Answer</summary>

```js
function flattenRecursive(arr) {
  let result = []
  for (let item of arr) {
    if (Array.isArray(item)) {
      result.push(...flattenRecursive(item))
    } else {
      result.push(item)
    }
  }
  return result
}

// Test
const nestedArray = [1, [2, 3, [4, 5]], 6, [[7], [8, 9]]]
console.log(flattenRecursive(nestedArray)) // Expected output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

</details>

---

9. **Implement `call()`, and `apply()`** Understand the context (`this`) manipulation.

<details>
<summary>View Answer</summary>

```js
// syntax
function.call(thisArg, arg1, arg2, ...);
```

```js
Function.prototype.myCall = function (context, ...args) {
  // Both globalThis and window are same
  context = context || globalThis // Use the global object if no context is provided.

  // Create a unique temporary function name using Symbol
  const tempFn = Symbol('temp')

  // Temporarily assign the function to the context
  context[tempFn] = this

  // Invoke the function using the context
  const result = context[tempFn](...args)

  // Clean up by deleting the temporary function reference
  delete context[tempFn]

  return result
}

// Example:
function introduce(name, age) {
  console.log(`Hi, I am ${name}, ${age} years old from ${this.city}.`)
}

const person = {
  city: 'Los Angeles',
}

introduce.myCall(person, 'John', 30)
// Outputs: Hi, I am John, 30 years old from Los Angeles.
```

```js
Function.prototype.myApply = function (context, args) {
  context = context || window // Use the global object if no context is provided.

  // Create a unique temporary function name to avoid overriding existing properties
  const tempFn = Symbol('temp')

  // Temporarily assign the function to the context
  context[tempFn] = this

  // Invoke the function using the context
  // We're using the spread operator here to spread the elements of the args array
  const result = context[tempFn](...args)

  // Clean up by deleting the temporary function reference
  delete context[tempFn]

  return result
}

//Example
function greet(name, age) {
  console.log(
    `Hello, my name is ${name} and I am ${age} years old, and I live in ${this.city}.`
  )
}

const person = {
  city: 'New York',
}

greet.myApply(person, ['Alice', 25]) // Outputs: Hello, my name is Alice and I am 25 years old, and I live in New York.
```

</details>

---

10. **Find a first pair whose sum is zero using indexing**

```js
function getSumPairZero(array) {
  let left = 0
  let right = array.length - 1
  while (left < right) {
    sum = array[left] + array[right]
    if (sum === 0) {
      return [array[left], array[right]]
    } else if (sum > 0) {
      right--
    } else {
      left++
    }
  }
}
const result = getSumPairZero([-5, -4, -3, -2, -1, 0, 2, 4, 6, 8])
console.log(result)
```

---

11. **Find the largest elements from the 2 dimensional array**

```js
function findLargestElement(matrix) {
  if (!matrix.length || !matrix[0].length) return null // If empty array

  let max = matrix[0][0] // Assume the first element is the largest

  for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix[i].length; j++) {
      if (matrix[i][j] > max) {
        max = matrix[i][j]
      }
    }
  }

  return max
}

// Test
const arr = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
]
console.log(findLargestElement(arr)) // Output: 9
```

---

12. **Write a function that performs a deep comparison between two values to determine if they are equivalent** Recursion, considering types, properties, and values.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. if obj1 === obj2 return true
2. if obj1 or obj2 are null or not an object return false
3. We need keys of the object and object always changes due to recursion
   ex: Object.keys(obj1) returns an array
4. now do for of loop of keys array
5. Each and every key will be passed inside the recursive function ex: obj1(key)

```js
function deepEqual(a, b) {
  // If both are the exact same value (strict equality), they are equal
  if (a === b) return true

  // If either of them is null or not an object, they aren't deep equal
  if (
    a === null ||
    b === null ||
    typeof a !== 'object' ||
    typeof b !== 'object'
  )
    return false

  // Get the keys of both objects
  let keysA = Object.keys(a),
    keysB = Object.keys(b)

  // If they have a different number of keys, they are not deep equal
  if (keysA.length !== keysB.length) return false

  // Check if every key-value pair in `a` matches that in `b`
  for (let key of keysA) {
    if (!keysB.includes(key) || !deepEqual(a[key], b[key])) return false
  }

  return true
}

let obj1 = { a: 1, b: [1, 2, 3], c: { d: 4, e: 5 } }
let obj2 = { a: 1, b: [1, 2, 3], c: { d: 4, e: 6 } }
console.log(deepEqual(obj1, obj2))
```

</details>

---

13. **Implement an EventEmitter class** Use an object to manage events and callbacks.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. this.events is an object inside constructor function
2. on, off receives eventName and callback as arguments and we check eventName is present or not in the this.events object ex: this.events[eventName]
3. for `on` method, if there is no eventName then create an array ex: this.events[eventName] = [] and push the callback (2nd arg) inside array
4. off is to filter inside, emit is to loop inside

```js
class EventEmitter {
  constructor() {
    // Object to manage events and callbacks
    this.events = {}
  }

  // Register an event with a callback
  on(eventName, callback) {
    if (!this.events[eventName]) {
      this.events[eventName] = []
    }
    this.events[eventName].push(callback)
  }

  // Trigger an event
  emit(eventName, ...args) {
    if (this.events[eventName]) {
      this.events[eventName].forEach((callback) => {
        callback(...args)
      })
    }
  }

  // Remove a specific callback for an event
  off(eventName, callback) {
    if (this.events[eventName]) {
      this.events[eventName] = this.events[eventName].filter(
        (cb) => cb !== callback
      )
    }
  }

  // Remove all callbacks for an event
  removeAllListeners(eventName) {
    if (this.events[eventName]) {
      delete this.events[eventName]
    }
  }
}

// Example usage:
const emitter = new EventEmitter()
emitter.on('data', (data) => {
  console.log('Received data:', data)
})
emitter.on('userJoined', (...usernames) => {
  usernames.forEach((userName) => {
    console.log(`${userName} has joined the chat.`)
  })
})

emitter.emit('data', { test: 123 }) // Outputs: Received data: { test: 123 }
emitter.emit('userJoined', 'Alice', 'Blice', 'Clice')
// Outputs:
// Alice has joined the chat.
// Blice has joined the chat.
// Clice has joined the chat.
```

</details>

---

14. **Convert a callback-based function to a promise-based one** Wrap the function using `new Promise()`.

<details>
<summary>View Answer</summary>

```js
// Callback code
const request = require('request')

function fetchUserData(userId, callback) {
  const url = `https://api.example.com/user/${userId}`

  request(url, (error, response, body) => {
    if (error) {
      callback(error, null)
    } else if (response.statusCode !== 200) {
      callback(new Error(`Received status code ${response.statusCode}`), null)
    } else {
      callback(null, JSON.parse(body))
    }
  })
}

// Usage:
fetchUserData(123, (error, data) => {
  if (error) {
    console.error(error)
  } else {
    console.log(data)
  }
})
```

```js
// Promise Conversion
const request = require('request')

function fetchUserData(userId) {
  return new Promise((resolve, reject) => {
    const url = `https://api.example.com/user/${userId}`

    request(url, (error, response, body) => {
      if (error) {
        reject(error)
      } else if (response.statusCode !== 200) {
        reject(new Error(`Received status code ${response.statusCode}`))
      } else {
        resolve(JSON.parse(body))
      }
    })
  })
}

// Usage:
fetchUserData(123)
  .then((data) => {
    console.log(data)
  })
  .catch((error) => {
    console.error(error)
  })
```

</details>

---

**15. uncompress string**

```js
//Example
uncompress('3(ab)') // 'ababab'
uncompress('3(ab2(c))') // 'abccabccabcc'
```

```js
function uncompress(s) {
  let i = 0

  function helper() {
    let result = ''
    let num = 0

    while (i < s.length) {
      if (s[i].match(/[0-9]/)) {
        num = num * 10 + parseInt(s[i])
        i++
      } else if (s[i] === '(') {
        i++ // Move past '('
        const substring = helper()

        //this below repeat line will be called at last after executing everything inside the brackets
        result += substring.repeat(num)

        num = 0 // Reset num for next sequence
      } else if (s[i] === ')') {
        i++ // Move past ')'
        return result
      } else {
        result += s[i]
        i++
      }
    }

    return result
  }

  return helper()
}

// Test
console.log(uncompress('3(ab)')) // 'ababab'
console.log(uncompress('3(ab2(c))')) // 'abccabccabcc'
console.log(uncompress('5(5(ab)2(c)))')) // 'abababababccabababababccabababababccabababababccabababababcc'
```

---

16. **Create a function to calculate the sum of all the numbers in a jagged array**

```js
function sumArray(ar) {
  var sum = 0
  for (var el of ar) {
    if (Array.isArray(el)) {
      el = sumArray(el) //recursion
    }
    sum += el
  }
  return sum
}
console.log(sumArray([1, 2, [3, [4], [5, 6]], [7]])) //28
```

---

17. **Implement memoization for recursive functions** Cache results in a higher-order function.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. write a fibonacci function which will be our example for memoization
2. fiboannci using recursion is simple, one condition checks if n<=1 then return n
3. in other scenarios it would return fib(n-1)+fib(n-2)
4. Memoization function requires cache object and a key
5. generate a key based on the number (ex: 12)
6. if cache[key]!==undefined then cache[key]= result and return the result
7. result is fib function which takes args

```js
const memoize = (func) => {
  const cache = {}

  return (...args) => {
    const key = JSON.stringify(args)
    if (cache[key] !== undefined) {
      return cache[key]
    }
    const result = func(...args)
    cache[key] = result
    return result
  }
}

// Example: Recursive Fibonacci with memoization
const fib = (n) => {
  // if n = 0 or 1, it will return 0 or 1
  if (n <= 1) {
    return n
  }
  return fib(n - 1) + fib(n - 2)
}

const memoizedFib = memoize(fib)
console.log(memoizedFib(12)) // Output: 144
console.log(memoizedFib(12)) // Output: 144
```

</details>

---

18. **Check if an object is empty** Use `Object.keys()` and check length.

<details>
<summary>View Answer</summary>

```js
const isEmptyObj = (obj) => {
  return Object.keys(obj).length === 0
}
```

Ex:

```js
const obj1 = {}
console.log(isEmptyObj(obj)) //true
```

```js
const obj2 = { name: 'John' }
console.log(isEmpty(obj2)) // false
```

</details>

---

19. **Write a function to retrieve query parameters from a URL string** Use regular expressions or URLSearchParams.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. whatever the url you are getting as a argument, pass that inside new URL(passed_argument)
2. once you log the above stored variable you would see different fields in the object. (ex: below image)
   ![image](https://github.com/saiteja-gatadi1996/notes/assets/42731246/25b1c75c-ab75-4efb-bd33-af45edce27b8)

3. take the `search` field using `.search` notation and pass that inside URLSearchParams and store this in a another variable called params or anything
4. do a for of loop on the params.entries() and we need key, value from the params.entries()
5. store them inside a result obj

```js
const getQueryParams = (url) => {
  const urlObj = new URL(url)
  const params = new URLSearchParams(urlObj.search)
  const result = {}

  for (const [key, value] of params.entries()) {
    result[key] = value
  }
  return result
}

const queryParams = getQueryParams('https://example.com/page?name=John&age=25')
console.log(queryParams)
```

</details>

---

20. **Determine if the given variable is a truthy or falsy value in JavaScript** Direct boolean conversion or ternary checks.

<details>
<summary>View Answer</summary>

```js
const isTruthy = (value) => !!value

console.log(isTruthyTernary(1)) // true
console.log(isTruthyTernary(0)) // false
console.log(isTruthyTernary('hello')) // true
console.log(isTruthyTernary('')) // false
```

</details>

---

21. **Find the longest word length**

<details>
<summary>View Answer</summary>

```js
const words = ['apple', 'banana', 'cherry', 'dragonfruit', 'elderberry']

const longestWordLength = words.reduce((maxLength, word) => {
  const currentLength = word.length
  return currentLength > maxLength ? currentLength : maxLength
}, 0)

console.log(longestWordLength) // Output: 11
```

</details>

---

22. **Implement a function that can flatten an array with any level of nested arrays** Recursive flattening with Array.isArray() check.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. accept array as an arugment
2. put a for of loop, you will get an item
3. check if that item is Array.isArray(item), if yes result.push(...recursiveFuncti(item))
4. else result.push(item)

```js
const flattenArray = (arr) => {
  let result = []

  for (const item of arr) {
    if (Array.isArray(item)) {
      result.push(...flattenArray(item)) //push method, using the spread operator allows us to push each individual element of the array returned by the recursive call into the result array.
    } else {
      result.push(item)
    }
  }

  return result
}

const nestedArray = [1, [2, [3, [4, 5], 6], 7], 8]
console.log(flattenArray(nestedArray)) // [1, 2, 3, 4, 5, 6, 7, 8]
```

</details>

---

23. **Write a function that capitalizes the first letter of each word in a string**

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- Using regex pattern we can achieve this
- backslash (/) says that it is starting or ending your code
- \b matches the position where a new word starts
- \w matches the first word character immediately after the word boundary
- g is a global flag, meaning the above pattern will be searched for throughout the entire string (not just the first occurrence).

```js
function captilizeFirstOccurrence(str) {
  return str.replace(/\b\w/g, (char) => char.toUpperCase())
}

console.log(captilizeFirstOccurrence('hello world! this is a test string.'))
```

</details>

---

24. **To check weather perfect number or not**

```js
function is_perfect(number) {
  var temp = 0
  for (var i = 1; i <= number / 2; i++) {
    if (number % i === 0) {
      console.log(i) //1,2,4,7,14
      temp += i
    }
  }
  if (temp === number && temp !== 0) {
    console.log('It is a perfect number.')
  } else {
    console.log('It is not a perfect number.')
  }
}
is_perfect(28)
```

---

25. **Find the longest word**

<details>
<summary>View Answer</summary>

```js
const longestWord = words.reduce((longestWord, word) => {
  return word.length > longestWord.length ? word : longestWord
}, '')

console.log(longestWord) // Output: 'dragonfruit'
```

</details>

---

26. **String Compression**

```js
function stringCompression(str) {
  if (str.length == 0) {
    console.log('Please enter valid string.')
    return
  }
  var output = ''
  var count = 0
  for (var i = 0; i < str.length; i++) {
    count++
    if (str[i] != str[i + 1]) {
      //if a is not equal to b
      output += str[i] + count //a+4
      count = 0 //for b it will start from zero
    }
  }
  console.log(output)
}
stringCompression('') //Please enter valid string.
stringCompression('aaaa') //a4
stringCompression('aaaabbc') //a4b2c1
stringCompression('aaaabbcaabb') //a4b2c1a2b2
```

---

27. **Detect if the given variable is an array or not** , use Array.isArray() or `instanceof` checks.

<details>
<summary>View Answer</summary>

```js
const arr = [1, 2, 3]

if (Array.isArray(arr) && arr instanceof Array) {
  console.log('The variable is an array.')
} else {
  console.log('The variable is not an array.')
}
```

</details>

---

28. **Write a function to convert a string from `CamelCase` to `snake_case`** Use Regular expressions with string replace.

<details>
<summary>View Answer</summary>

```js
function camelToSnakeCase(str) {
  return str.replace(/([a-z0-9]|(?=[A-Z]))([A-Z])/g, '$1_$2').toLowerCase()
}

const camelCaseStr = 'saitejaGatadiIsGoodBoy'
const snakeCaseStr = camelToSnakeCase(camelCaseStr)
console.log(snakeCaseStr)
```

</details>

---

29. **Write a function that formats a number as a currency string (e.g., "1234.56" to "$1,234.56")**

- Use toLocaleString or manual string manipulation.

<details>
<summary>View Answer</summary>
```js
function formatCurrency(amount) {
  return amount.toLocaleString('en-US', {
    style: 'currency',
    currency: 'USD',
  })
}
const number = 1234.56
const currencyString = formatCurrency(number)
console.log(currencyString) // Outputs: "$1,234.56"
```

</details>

---

30. **Create a pub-sub (publisher-subscriber) pattern implementation**. Manage topics and subscribers in an object.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- publish function takes two params (topic, message)
- subscribe function takes two params (topic, function or callback function)
- in subscribe function check if the topic is already there inside the topics object, if not topics[topic] = []
- inside the subscribe you can write logic for unsubscribe by delete topics[topic][index]
- you can get the index by topics[topic].push(listener) will return 1 and do the -1 which returns 0
- publish checks if the topic is present by using less than 1 conditon, else return nothing
- just do the forEach loop topics[topic].forEach and you will have the passed function as a item and return that if it is not undefined else return {}

```js
const createPubSub = () => {
  const topics = {}

  const subscribe = (topic, listener) => {
    if (!topics[topic]) topics[topic] = []

    // push returns 1, so it looks like 1 - 1 = 0
    const index = topics[topic].push(listener) - 1

    return {
      remove: () => {
        delete topics[topic][index]
      },
    }
  }

  const publish = (topic, info) => {
    if (!topics[topic] || topics[topic].length < 1) return

    // during looping, each and every item or listener is the callback function that is passed as a 2nd argument
    topics[topic].forEach((listener) =>
      listener(info !== undefined ? info : {})
    )
  }

  return {
    subscribe,
    publish,
  }
}

// Example Usage
const pubSub = createPubSub()

const subscription = pubSub.subscribe('example', (data) => {
  console.log(`Received data: ${JSON.stringify(data)}`)
})

pubSub.publish('example', { message: 'Hello, World!' })

// To unsubscribe
subscription.remove()
```

</details>

---

31. **Detect data type in JavaScript**

```js
//Example Inputs
detectType(1) // 'number'
detectType(new Map()) // 'map'
detectType([]) // 'array'
detectType(null) // 'null'
```

```js
function detectType(value) {
  if (value === null) return 'null'

  // Use the 'typeof' operator for primitive types
  const type = typeof value
  if (type !== 'object' && type !== 'function') return type

  // Use the Object.prototype.toString.call() method for complex types
  const objectType = Object.prototype.toString.call(value)

  if (objectType === '[object Array]') return 'array'
  if (objectType === '[object Map]') return 'map'
  //... add more detections as needed

  return 'unknown'
}

// Test the function
console.log(detectType(1)) // 'number'
console.log(detectType(new Map())) // 'map'
console.log(detectType([])) // 'array'
console.log(detectType(null)) // 'null'
```

---

32. **Check if a DOM element is a child of another DOM element**

<details>
<summary>View Answer</summary>

```js
// contains
const isChildOf = (child, parent) => parent.contains(child)

//closest
const isChildOf = (child, parent) => child.closest(parent.tagName) === parent

// Ex:
const parent = document.getElementById('parent')
const child = document.getElementById('child')

console.log(isChildOf(child, parent)) // It will log true if child is a descendant of parent, otherwise false
```

</details>

---

33. **Write a function to simulate the `new` operator in JavaScript**

<details>

<summary>View Answer</summary>

```js
function newOperator(Constructor, ...args) {
  // Step 1: Create a new object with the constructor's prototype
  const obj = Object.create(Constructor.prototype)

  // Step 2: Apply the constructor to the new object using call() instead of apply()
  const result = Constructor.call(obj, ...args)

  // Step 3: Return the object, unless the constructor returns an object
  return result && typeof result === 'object' ? result : obj
}

// Example usage:
function Person(name, age) {
  this.name = name
  this.age = age
}

Person.prototype.sayHello = function () {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`)
}

const john = newOperator(Person, 'John', 30)
john.sayHello() // Output: Hello, my name is John and I am 30 years old.
```

</details>

---

34. **Write a function to convert a NodeList to an array**

- Use Array.from() or spread operator.

<details>
<summary>View Answer</summary>

```js
function convertNodeListIntoArray(nodeList) {
  return [...nodeList]
  // return Array.from(nodeList)
}

const divs = document.querySelectorAll('div') // NodeList
const divsArray = convertNodeListIntoArray(divs)
console.log('divsInArray', divsArray)
```

</details>

---

35. **Implement a function to get a deep value from an object using a string, e.g., `get(obj, 'a.b.c')`**

- Split the string and reduce it over the object.

<details>
<summary>View Answer</summary>

```js
const deepValueInObj = (obj, path) => {
  return path
    .split('.')
    .reduce(
      (accumulator, currentValue) =>
        accumulator && accumulator[currentValue] !== undefined
          ? accumulator[currentValue]
          : null,
      obj
    )
}
// Example usage:
const obj = {
  a: {
    b: {
      c: 42,
    },
  },
}

console.log(deepValueInObj(obj, 'a.b.c')) // Output: 42
console.log(deepValueInObj(obj, 'a.b.x')) // Output: null
```

</details>

---

36. **Write a function to check if a JavaScript version supports ES6 features**

- Check specific features or functions like `let`, `const`, or arrow functions.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- this will be an array, so you can store in a varaible ex: const array = Object(this)
- if the callback.call is true return the element ex: const element = array[i]

```js
function supportsES6() {
  try {
    // Test let/const
    eval('let foo = null; const bar = null;')

    // Test arrow function
    eval('() => {};')

    return true
  } catch (e) {
    return false
  }
}

console.log(supportsES6()) // Output: true if ES6 is supported, false otherwise
```

</details>

---

37. **implement JSON.parse()**

<strong>TOUGH ONE, takes lot of time</strong>

```js
function parse(str) {
  if (str === '') {
    throw Error()
  }
  if (str[0] === "'") {
    throw Error()
  }
  if (str === 'null') {
    return null
  }
  if (str === '{}') {
    return {}
  }
  if (str === '[]') {
    return []
  }
  if (str === 'true') {
    return true
  }
  if (str === 'false') {
    return false
  }
  if (str[0] === '"') {
    return str.slice(1, -1)
  }
  if (+str === +str) {
    return Number(str)
  }
  if (str[0] === '{') {
    return str
      .slice(1, -1)
      .split(',')
      .reduce((acc, item) => {
        const index = item.indexOf(':')
        const key = item.slice(0, index)
        const value = item.slice(index + 1)
        acc[parse(key)] = parse(value)
        return acc
      }, {})
  }
  if (str[0] === '[') {
    return str
      .slice(1, -1)
      .split(',')
      .map((value) => parse(value))
  }
}
```

---

38. **Write a function that can transpose a 2D matrix (array of arrays)**

- Nested loops with swapped indices.

<details>
<summary>View Answer</summary>

```js
function transpose(matrix) {
  const rows = matrix.length
  const cols = matrix[0].length
  const transposed = Array.from({ length: cols }).map(() => Array(rows).fill(0))

  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      transposed[j][i] = matrix[i][j]
    }
  }

  return transposed
}

// Example usage:
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
]

const transposedMatrix = transpose(matrix)
console.log(transposedMatrix)
```

```js
//shorter syntax:
function transpose(matrix) {
  const rows = matrix.length
  const cols = matrix[0].length
  const transposed = Array.from({ length: cols }, (_, i) =>
    Array.from({ length: rows }, (_, j) => matrix[j][i])
  )
  return transposed
}

// Example usage:
const matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
]

const transposedMatrix = transpose(matrix)
console.log(transposedMatrix)
```

</details>

---

39. **Implement a curry function in JavaScript**

- Return a function that, when called with fewer arguments than it expects, returns a function that waits for more.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- have a look at the way you provided ex: sum function is provided as a param to curry function, this curry(sum) is provided into a curriedSum variable and curriedSum is going to get the args
- so if you want the args.length you will get it from first return (ex: return function curried(...args))
- if args.length is same with the sum function or desired output function then desired function.apply(this, args)
- else, concat the args with leftOverArgs (ex: return curried.apply(this, args.concat(remainingArgs)))

```js
function curry(fn) {
  //fn is the sum function which has 3 arguments, so fn.length = 3
  return function curried(...args) {
    //args are the curriedSum provided arguments, in the first example it is 1, so it fails if conditon
    if (args.length >= fn.length) {
      // invokes the function sum with those arguments using the apply method and returns the result
      // below will be called at final, ex: else condition does the job to concatenate the provided args with all the left over arguments until it matches with the sum function in our case
      return fn.apply(this, args)
    } else {
      // if curriedSum doesn't have enough arguments, it returns a new function that expects the remaining arguments.
      // This new function when invoked calls `curried` with both the original and new arguments concatenated together
      return function (...remainingArgs) {
        return curried.apply(this, args.concat(remainingArgs))
      }
    }
  }
}

// Example usage:
function sum(a, b, c) {
  return a + b + c
}

const curriedSum = curry(sum)

console.log(curriedSum(1)(2)(3)) // Output: 6
console.log(curriedSum(1, 2)(3)) // Output: 6
console.log(curriedSum(1, 2, 3)) // Output: 6
```

</details>

---

40. **Write a function that can perform batch async operations by taking in an array of promises and a batch size**

- Manage promise execution in chunks using `Promise.all()`.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- as we have to pass the promise functions in batches, we have to slice them (ex: slice the promise functions)
- await these sliced functions are part of array, do await Promise.all(slicedFunctions.map((eachSlicedFunction)=> eachSlicedFunction()))
- as we invoke or call the functions in batches, don't forget to add result.concat upfront

```js
async function batchProcessPromises(tasks, batchSize) {
  let result = []

  for (let i = 0; i < tasks.length; i += batchSize) {
    console.log('i', i)
    const batch = tasks.slice(i, i + batchSize) // ex: [f, f,f ] sliced to [f, f]
    // mapping over batch sliced functions and calling each function to get the promises they return
    // result at first has the first batch and then it concatenates with following batch, similarly batch.map in this batch is the updated slice function
    result = result.concat(await Promise.all(batch.map((task) => task())))
  }

  return result
}

// Real-time example usage:
const urls = [
  'https://jsonplaceholder.typicode.com/posts/1',
  'https://jsonplaceholder.typicode.com/posts/2',
  'https://jsonplaceholder.typicode.com/posts/3',
  // ... add more URLs as needed
]

const fetchPromises = urls.map(
  (url) => () => fetch(url).then((response) => response.json()) // [f, f, f]
)

batchProcessPromises(fetchPromises, 2)
  .then((results) => {
    console.log('All data fetched in batches:', results)
  })
  .catch((error) => {
    console.error('An error occurred:', error)
  })
```

</details>

---

41. **Create a simple observer pattern implementation**

- Define subjects and observers and manage notifications.

---

42. **Implement a chainable function: `add(1)(2)(3)....()`, where a final empty invocation returns the sum**

- Return a function from each invocation and use toString or valueOf for final computation.

<details>
<summary>View Answer</summary>

Certainly! You can achieve this by returning a function from each invocation that keeps track of the sum so far. When it's invoked with no arguments, you can use the `toString` or `valueOf` method to compute and return the final sum. Here's an example using `toString`:

```javascript
function add(n) {
  let sum = n

  const addNext = (next) => {
    if (next !== undefined) {
      sum += next
      return addNext
    }
    return sum
  }

  addNext.toString = () => sum

  return addNext
}

// Test
console.log(add(1)(2)(3)()) // Output: 6
console.log(add(1)(2)(3)(4)(5)()) // Output: 15
```

Explanation:

- The `add` function takes a number `n` and initializes a `sum` variable with it.
- It then defines an `addNext` function that takes the next number `next`. If `next` is provided, it adds it to `sum` and returns `addNext` again, allowing for chaining. If `next` is not provided (i.e., the function is invoked with no arguments), it returns the current `sum`.
- We override the `toString` method of `addNext` to return the current `sum`. This allows us to compute the final sum when the function is used in a context that requires a string, like `console.log`, or when it's invoked with no arguments at the end of the chain.
- Finally, `add` returns `addNext`, starting the chain
</details>

---

43. **Implement a function that can get the last N elements from an array**

- Use `slice()`.

<details>
<summary>View Answer</summary>

```js
function getLastNElements(array, n) {
  return n >= 0 ? array.slice(Math.max(0, array.length - n)) : []
}

// Test
const myArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
console.log(getLastNElements(myArray, 5)) // Output: [6, 7, 8, 9, 10]
```

</details>

---

44. **Write a function to compute the factorial of a number using only ternary operators**

- Recursive approach with the conditional (ternary) operator.

<details>
<summary>View Answer</summary>

```js
const factorial = (n) => {
  n === 0 ? 1 : n * factorial(n - 1)
}

console.log(factorial(5))
```

</details>

---

45. **Check if a given string is a valid JSON without using `try/catch` or external libraries**

<details>
<summary>View Answer</summary>

```js
function looksLikeJSON(str) {
  if (typeof str !== 'string') return false

  const trimmed = str.trim()

  const patterns = [
    { starts: '{', ends: '}' },
    { starts: '[', ends: ']' },
  ]

  if (
    !patterns.some(
      (pattern) =>
        trimmed.startsWith(pattern.starts) && trimmed.endsWith(pattern.ends)
    )
  ) {
    return false
  }

  return true
}

// Test
console.log(looksLikeJSON('{"name": "Alice"}')) // Should log true
console.log(looksLikeJSON('[1, 2, 3]')) // Should log true
console.log(looksLikeJSON('Just a regular string')) // Should log false
```

</details>

---

46. **Implement a function that can create a range generator (using ES6 generator functions)**

- Use the `function*` declaration and `yield`.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- a generator function which takes start and end as params, and it has a basic for loop which has start and end and instead of returning you are yielding (ex: yield i)
- store this function as a variable
- do a for of loop on this range (which is a generator function) and take each and every number and log it

```js
function* rangeGenerator(start, end) {
  for (let i = start; i <= end; i++) {
    yield i
  }
}
const range = rangeGenerator(1, 5)

for (let number of range) {
  console.log(number)
}
```

</details>

---

47. **Implement clearAllTimout() polyfill**

```js
//Ex

setTimeout(func1, 10000)
setTimeout(func2, 10000)
setTimeout(func3, 10000)

// all 3 functions are scheduled 10 seconds later
clearAllTimeout()

// all scheduled tasks are cancelled.
```

```js
let timeouts = []

// Override the native setTimeout function
// This is done so that we can later use the original setTimeout function while still overriding it with our custom behavior.
const originalSetTimeout = window.setTimeout

// Any subsequent calls to setTimeout will now use this new function.
window.setTimeout = function (fn, delay) {
  const timeoutId = originalSetTimeout(fn, delay)
  timeouts.push(timeoutId)
  return timeoutId
}

function clearAllTimeout() {
  for (const timeoutId of timeouts) {
    clearTimeout(timeoutId)
  }
  timeouts = [] // Reset the timeouts array
}

// Example usage:
const id1 = setTimeout(() => {
  console.log('Timeout 1')
}, 1000)

const id2 = setTimeout(() => {
  console.log('Timeout 2')
}, 2000)

clearAllTimeout() // This will prevent both timeouts from executing
```

---

48. **Calculate the factorial of the largest number in the array**

<details>
<summary>View Answer</summary>

```js
const numbers = [5, 2, 8, 4, 3]

const largestFactorial = numbers.reduce((largest, num) => {
  const currentFactorial = Array.from({ length: num })
    .map((_, i) => i + 1)
    .reduce((fact, val) => fact * val, 1)

  return currentFactorial > largest ? currentFactorial : largest
}, 1)

console.log(largestFactorial) // Output: 40320 (8!)
```

</details>

---

49. **Implement a function to get the maximum occurring character in a string** Use a hash map to store character counts.

<details>
<summary>View Answer</summary>
<strong>Approach Taken:</strong>
- given the string, do the for of loop and get each and every character and check that char exists or not in that object
- if it exists do the +1 else it has a or conditon with 0
- now do another for in loop (for keys) on the object that you have stored and check that char in that object is greater than the maxCount (by default it is zero)
- if it is greater then maxCount will be the that value
- and maxChar is that char which you are traversing
- atlast retur the object

```js
function getMaxOccurringCharWithCount(str) {
  let maxCount = 0
  let maxChar = ''
  const charCountMap = {}

  for (let char of str) {
    charCountMap[char] = (charCountMap[char] || 0) + 1
  }

  for (let char in charCountMap) {
    if (charCountMap[char] > maxCount) {
      maxCount = charCountMap[char]
      maxChar = char
    }
  }

  return {
    maxChar,
    maxCount,
  }
}

const output = getMaxOccurringCharWithCount('saiteja')
console.log('output', output) // { "maxChar": "a","maxCount": 2}
```

</details>

---

50. **Write a function to calculate the number of days between two dates** Convert both dates to milliseconds and find the difference.

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- accept the two dates
- pass them in the new Date(date1)
- do the .getTime() for them to achieve in milliseconds (ex: new Date('2023-10-08').getTime())
- Use Math.abs( difference of two times ) (ex: Math.abs(time2 -time 1)) for precision
- use this precision value to divide with ms*s*min*hours pattern (ex: 1000*60*60*24)

```js
function daysBetweenDates(date1, date2) {
  // Convert both dates to milliseconds
  const time1 = date1.getTime()
  const time2 = date2.getTime()

  // Find the difference in milliseconds
  const differenceInMilliseconds = Math.abs(time1 - time2)

  // Convert the difference to days
  const differenceInDays = differenceInMilliseconds / (1000 * 60 * 60 * 24)

  return differenceInDays
}

// Test the function with two dates
const date1 = new Date('2023-10-01')
const date2 = new Date('2023-10-09')
const numberOfDays = daysBetweenDates(date1, date2)
console.log('Number of days between the two dates:', numberOfDays)
```

```js
// solution 2- shorter syntax

function daysBetweenDates(...dates) {
  const [time1, time2] = dates.map((date) => new Date(date).getTime())
  const differenceInMilliseconds = Math.abs(time1 - time2)
  return differenceInMilliseconds / (1000 * 60 * 60 * 24)
}

// Test the function with two dates
const numberOfDays = daysBetweenDates('2023-10-01', '2023-10-09')
console.log('Number of days between the two dates:', numberOfDays)
```

</details>

---

**51. Print the duplicates in an array**

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

- When you have a duplicates array as a input, use this same array to print what are the duplicates as output by using filter condition(as it removes undefined values also)
- By using <strong>new Set logic</strong> you will get unique values in Set object and now use the .has, .delete methods to check the uniqueValues object.
- By the time when duplicates array has a duplicate item, the uniqueValues has deleted from its object and we are returning that as part of else logic.

```js
const toFindDuplicates = (duplicatesArray) => {
  const uniqueArrayElements = new Set(duplicatesArray)
  console.log('find', uniqueArrayElements) // Set {1, 2, undefined, 5, 3, 4}

  const filteredElements = duplicatesArray.filter((item) => {
    if (uniqueArrayElements.has(item)) {
      uniqueArrayElements.delete(item)
    } else {
      return item
    }
  })
  console.log('find filteredElements', filteredElements) // [1, 3, 5]
}

const newArray = [1, 2, 1, , 5, 3, 4, 3, 5]
const duplicateElements = toFindDuplicates(newArray)
```

</details>

---

**52. Reverse the words in the string without using the `split` and `reverse`:**

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

1. For reversing, start a for loop from `let i = str.length; i>=0; i--`
2. Each and evey character from the reverse has to be appended to the word (to achieve desired output) and that has to be stored in word itself (ex: word = str[i] + word)
3. if it encounters the space then the word till then (ex: SaiTeja) has to be appended with a Space and stored into a result. `(Ex: result+=word + " ")`
4. make your word as an empty string so that next time `am` will be your word and your result will be previous result + `am` word
5. The tricky part of this solution is your first word in the string (ex: I in our case) will never be part of else condition.
6. Due to this reason, you have append your word to your result and return it

```js
let a = 'I am SaiTeja'
const reverseWords = (str) => {
  let result = '',
    word = ''
  for (let i = str.length - 1; i >= 0; i--) {
    if (str[i] !== ' ') {
      word = str[i] + word
    } else {
      result += word + ' '
      word = ''
    }
  }
  result += word // append the last word
  return result
}

console.log(reverseWords(a)) // "SaiTeja am I"
```

</details>

---

**53. Print only uniques inside a string variable**

<details>
<summary>View Answer</summary>

<strong>Approach Taken:</strong>

_You can achieve this by following these steps:_

1. Put a for loop for the given input string to traverses each and every string Ex: `a[i]`
2. Put another for loop for `result` string to check if `inputString[i] === result[j]`
3. If yes, maintain a state to print `isDuplicate = true` and break
4. Outside to 2nd for loop, inside the first for loop (write the if condtion to check isDuplicate is true or false)
5. If it is not duplicate then result will be added with the inputString[i]

Here's the code for the above logic:

```javascript
let inputString = 'saitejaisgoodboy'
let result = ''

for (let i = 0; i < inputString.length; i++) {
  let isDuplicate = false
  for (let j = 0; j < result.length; j++) {
    if (inputString[i] === result[j]) {
      isDuplicate = true
      break
    }
  }
  if (!isDuplicate) {
    result += inputString[i]
  }
}

console.log(result) // Outputs: "saitejgodby"
```

This solution iteratively checks each character of the string `a` against every character in the `result` string. If the character is not in the `result`, it is appended. Otherwise, it is skipped.

##### Solution 2: Using Set (O(n))

- The Set-based solution is the most performant with a time complexity of O(n).

```js
let a = 'saitejaisgoodboy'
let result = [...new Set(a)].join('')
console.log(result) // Outputs: "saitejgodby"
```

##### Solution 3: Using indexOf (O(n2))

- The outer loop runs n times. The indexOf method has a linear search which in the worst case is O(n). Hence, this method can also be O(n^2) in the worst case.

```js
let a = 'saitejaisgoodboy'
let result = ''

for (let i = 0; i < a.length; i++) {
  if (result.indexOf(a[i]) === -1) {
    result += a[i]
  }
}

console.log(result) // Outputs: "saitejgodby"
```

##### Solution 4: Using reduce (O(n2))

- The reduce function runs the callback for each element in the array, which is n times. The includes method also takes O(n) time in the worst case. Thus, this method is O(n^2) in the worst case.

```js
let a = 'saitejaisgoodboy'
let result = a.split('').reduce((acc, curr) => {
  if (!acc.includes(curr)) {
    acc += curr
  }
  return acc
}, '')

console.log(result) // Outputs: "saitejgodby"
```

</details>

---

**54. To count the number of vowels in a given string without using any inbuilt functions, you can do the following:**

<details>
<summary>View Answer</summary>

1. Create a string containing all the vowels.
2. Traverse through each character of the given string.
3. For each character, check if it is present in the vowel string.
4. If the character is a vowel, increment a counter.

Here's the code for the above logic:

```javascript
let a = 'saiteja'
let vowels = 'aeiouAEIOU' // considering both lowercase and uppercase vowels
let count = 0

for (let i = 0; i < a.length; i++) {
  for (let j = 0; j < vowels.length; j++) {
    if (a[i] === vowels[j]) {
      count++
      break
    }
  }
}

console.log(count) // Outputs: 3
```

This solution iteratively checks each character of the string `a` to see if it's a vowel by comparing it against each character in the `vowels` string. If it's a vowel, the counter is incremented.

---

<b>_To print which vowels are used in the string, you can make a few modifications:_</b>

1. Create a string containing all the vowels.
2. Traverse through each character of the given string.
3. For each character, check if it is present in the vowel string.
4. If the character is a vowel and it's not already identified (stored), store it.

Here's the code for the above logic:

```javascript
let a = 'saiteja'
let vowels = 'aeiouAEIOU'
let usedVowels = ''

for (let i = 0; i < a.length; i++) {
  for (let j = 0; j < vowels.length; j++) {
    if (a[i] === vowels[j]) {
      // Check if the vowel is already identified
      if (usedVowels.indexOf(a[i]) === -1) {
        usedVowels += a[i]
      }
      break
    }
  }
}

console.log(usedVowels) // Outputs: "aie"
```

In this solution, the `usedVowels` string keeps track of which vowels have been identified. The `indexOf` method is used to check if a vowel is already in the `usedVowels` string. If it's not, it's added to the `usedVowels` string.

##### Solution 2

```js
let a = 'saiteja'
let vowels = new Set('aeiouAEIOU')
let usedVowels = new Set()

for (let char of a) {
  if (vowels.has(char)) {
    usedVowels.add(char)
  }
}

console.log([...usedVowels].join('')) // Outputs: "aie"
```

</details>

---

**55. Write a debouncing function.**

<details>
<summary>View Answer</summary>

```javascript
function debounce(func, delay) {
  let timeout
  return (...args) => {
    clearTimeout(timeout)
    timeout = setTimeout(() => {
      console.log('Executing the actual function after delay')
      func(...args)
    }, delay)
  }
}

const debouncedLog = debounce(() => console.log('Hello after delay'), 1000)
debouncedLog()
```

</details>

---

**56. Implement a deep clone of an object.**

<details>
<summary>View Answer</summary>

```javascript
function deepClone(obj) {
  if (obj === null) return null
  if (typeof obj !== 'object') return obj

  if (Array.isArray(obj)) {
    return obj.map((item) => deepClone(item))
  }

  const clonedObj = {}
  for (const key in obj) {
    clonedObj[key] = deepClone(obj[key])
  }
  return clonedObj
}
```

</details>

---

**57. Implement a function to flatten a nested array.**

<details>
<summary>View Answer</summary>

```javascript
function flattenArray(arr) {
  return arr.reduce((acc, item) => {
    return Array.isArray(item)
      ? acc.concat(flattenArray(item))
      : acc.concat(item)
  }, [])
}
```

</details>

---

**58. Handle asynchronous operations like multiple API calls.**

<details>
<summary>View Answer</summary>

This example uses the Fetch API to handle multiple calls.

```javascript
const urls = ['https://api.example1.com', 'https://api.example2.com']

Promise.all(urls.map((url) => fetch(url)))
  .then((responses) =>
    Promise.all(responses.map((response) => response.json()))
  )
  .then((data) => {
    console.log(data) // Array of results from each API call
  })
  .catch((error) => console.error('Error in API calls:', error))
```

</details>

---

**59. Calculate the `average` score of students who `scored above 90`**

```js
// Input
const students = [
  { name: 'John', score: 85 },
  { name: 'Sarah', score: 92 },
  { name: 'Michael', score: 88 },
  { name: 'Emma', score: 95 },
  { name: 'Daniel', score: 90 },
]

// Expected output should be average of 95 and 92
```

<details>
<summary>View Answer</summary>

```js
const above90StudentsAverage = students
  .filter((student) => student.score > 90)
  .reduce((acc, student, i, arr) => acc + student.score / arr.length, 0)

console.log(above90StudentsAverage) // Output: 93.5 (average of 95 and 92)
```

</details>

---

**60. `Capitalize` the first letter of each word in the `array`**

```js
// Input
const strings = ['hello world', 'i am openai', 'welcome to javascript']
// Expected Output: ['Hello World', 'I Am Openai', 'Welcome To Javascript']
```

<details>
<summary>View Answer</summary>

```js
const newArr = strings.map((item) =>
  item.replace(/\b\w/g, (char) => char.toUpperCase())
)

console.log(newArr) // ["Hello World", "I Am Openai", "Welcome To Javascript"]
```

</details>

---

**61. Replace underscores with space and capitalize word**

```js
Input:
ui_dev_guide

output:
Ui Dev Guide

```

```js
function formatString(input) {
  return input
    .split('_') // Split the string by underscores.
    .map(
      (
        word // Capitalize the first letter of each word.
      ) => word.charAt(0).toUpperCase() + word.slice(1).toLowerCase()
    )
    .join(' ') // Join the words with spaces.
}

const input = 'ui_dev_guide'
const output = formatString(input)
console.log(output) // Outputs: "Ui Dev Guide"
```

---

**62. Find the occurrence in given array in JavaScript**

```js
Input:

[5,5,5,2,2,2,2,2,9,4]

Output:

{
  "2":5,
  "4":1,
  "5":3,
  "9":1,
}

```

```js
function countOccurrences(arr) {
  const occurrences = {}

  for (let num of arr) {
    if (!occurrences[num]) {
      occurrences[num] = 1 // If the number hasn't been counted yet, initialize it with 1
    } else {
      occurrences[num]++ // Otherwise, increment the count
    }
  }

  return occurrences
}

const input = [5, 5, 5, 2, 2, 2, 2, 2, 9, 4]
const output = countOccurrences(input)
console.log(output)
```

---

**63. Convert RGB to Hex**

<details>
<summary>View Answer</summary>

```js
function componentToHex(c) {
  var hex = c.toString(16)
  return hex.length == 1 ? '0' + hex : hex
}

function rgbToHex(r, g, b) {
  if (r > 255 || g > 255 || b > 255 || r < 0 || g < 0 || b < 0) {
    throw new Error('Invalid color component')
  }
  return '#' + componentToHex(r) + componentToHex(g) + componentToHex(b)
}

// Test the function with RGB color (255, 99, 71)
console.log(rgbToHex(255, 99, 71)) // Output: "#FF6347"
```

</details>

---

**64. Find the occurrences in given object**

```js
// Input
let people = [
  { name: 'Mary', gender: 'girl' },
  { name: 'Paul', gender: 'boy' },
  { name: 'John', gender: 'boy' },
  { name: 'Lisa', gender: 'girl' },
  { name: 'Bill', gender: 'boy' },
  { name: 'Maklatura', gender: 'girl' },
  { name: 'Sara', gender: 'girl' },
]

// Output
// boys: 3
```

```js
function countGender(people) {
  const genderCount = {}

  for (let person of people) {
    if (!genderCount[person.gender]) {
      genderCount[person.gender] = 1 // If the gender hasn't been counted yet, initialize it with 1
    } else {
      genderCount[person.gender]++ // Otherwise, increment the count
    }
  }

  return genderCount
}

const people = [
  { name: 'Mary', gender: 'girl' },
  { name: 'Paul', gender: 'boy' },
  { name: 'John', gender: 'boy' },
  { name: 'Lisa', gender: 'girl' },
  { name: 'Bill', gender: 'boy' },
  { name: 'Maklatura', gender: 'girl' },
  { name: 'Sara', gender: 'girl' },
]

const output = countGender(people)
console.log('boys:', output.boy) // Outputs: "boys: 3"
```

---

**65.Convert HEX Color to RGBA**

```js
function hexToRgba(hex, alpha = 1) {
  let cleanHex = hex.charAt(0) === '#' ? hex.slice(1) : hex

  if (cleanHex.length === 3) {
    cleanHex = cleanHex
      .split('')
      .map((char) => char + char)
      .join('')
  }

  if (cleanHex.length !== 6) {
    throw new Error('Invalid HEX color.')
  }

  const r = parseInt(cleanHex.substring(0, 2), 16)
  const g = parseInt(cleanHex.substring(2, 4), 16)
  const b = parseInt(cleanHex.substring(4, 6), 16)

  return `rgba(${r},${g},${b},${alpha})`
}

console.log(hexToRgba('#03F', 0.5)) // Outputs: "rgba(0,51,255,0.5)"
console.log(hexToRgba('#0033FF', 0.5)) // Outputs the same value
```

---

**66. add comma to number**

```js
function addComma(num) {
  if (Math.floor(num) !== num) {
    // If the number has a decimal part
    let parts = num.toString().split('.')
    return parts[0].toLocaleString('en-US') + '.' + parts[1]
  }
  return num.toLocaleString('en-US')
}

console.log(addComma(1)) // '1'
console.log(addComma(1000)) // '1,000'
console.log(addComma(-12345678)) // '-12,345,678'
console.log(addComma(12345678.12345)) // '12,345,678.12345'
```

---

**67. validate string of parentheses**

```js
//Example Inputs:

validate('{}[]()')
// true

validate('{[()]}')
// true

validate('{[}]')
// false, they are not in the right order

validate('{}}')
// false, last `}` is not paired with `{`
```

```js
function validate(s) {
  const stack = []
  const pairs = {
    ')': '(',
    ']': '[',
    '}': '{',
  }

  for (let char of s) {
    //first if condition gets satisfy if your traversing character matches with the keys only ex: },],)
    if (char in pairs) {
      // If the character is a closing parenthesis
      if (stack.pop() !== pairs[char]) {
        // The popped value from the stack should match the corresponding opening parenthesis (to get true)
        return false
      }
    } else {
      stack.push(char)
    }
  }

  return stack.length === 0 // The stack should be empty for a valid string
}

console.log(validate('{}[]()')) // true
console.log(validate('{[()]}')) // true
console.log(validate('{[}]')) // false
console.log(validate('{}}')) // false
```

---

**68. write your own `instanceof`**

```js
class A {}
class B extends A {}

const b = new B()
myInstanceOf(b, B) // true
myInstanceOf(b, A) // true
myInstanceOf(b, Object) // true

function C() {}
myInstanceOf(b, C) // false
C.prototype = B.prototype
myInstanceOf(b, C) // true
C.prototype = {}
myInstanceOf(b, C) // false
```

```js
function myInstanceOf(obj, constructor) {
  // If the constructor isn't a function or the prototype isn't defined, return false
  if (
    typeof constructor !== 'function' ||
    constructor.prototype === undefined
  ) {
    return false
  }

  // Loop through the prototype chain of the object
  let proto = Object.getPrototypeOf(obj)
  while (proto !== null) {
    if (proto === constructor.prototype) {
      return true // Found the constructor's prototype in the prototype chain
    }
    //checks inside prototype chain and goes back to while loop
    proto = Object.getPrototypeOf(proto)
  }

  return false // Didn't find the constructor's prototype in the prototype chain
}

// Test cases
class A {}
class B extends A {}

const b = new B()
console.log(myInstanceOf(b, B)) // true
console.log(myInstanceOf(b, A)) // true
console.log(myInstanceOf(b, Object)) // true

function C() {}
console.log(myInstanceOf(b, C)) // false
C.prototype = B.prototype
console.log(myInstanceOf(b, C)) // true
C.prototype = {}
console.log(myInstanceOf(b, C)) // false
```

---

**69. throttle Promises**

- Say you need to fetch some data through 100 APIs, and as soon as possible.

- If you use Promise.all(), 100 requests go to your server at the same time, which is a burden to low spec servers.

- Can you throttle your API calls so that always maximum 5 API calls at the same time?

- You are asked to create a general throttlePromises() which takes an array of functions returning promises, and a number indicating the maximum concurrent pending promises.

```js
//Scenario

throttleAsync(callApis, 5).then((data) => {
  // the data is the same as `Promise.all`
}).catch((err) => {
  // any error occurs in the callApis would be relayed here
})
By running above code, at any time, no more than 5 APIs are requested, so low spec servers are saved.
```

```js
function throttleAsync(tasks, maxConcurrent) {
  // Array to hold results
  let results = []

  // Recursive function to execute tasks
  function executeTasks(startIndex = 0) {
    // If all tasks have been started, return
    if (startIndex >= tasks.length) {
      return Promise.resolve()
    }

    // Slice tasks for concurrent execution
    let currentTasks = tasks.slice(startIndex, startIndex + maxConcurrent)

    // Execute current set of tasks and store results/errors
    return Promise.allSettled(currentTasks.map((task) => task())).then(
      (values) => {
        // Extract results from the settled promises
        values.forEach((value) => {
          if (value.status === 'fulfilled') {
            results.push(value.value)
          } else {
            // If any task rejects, we reject the main promise
            throw value.reason
          }
        })

        // Recursively call the next set of tasks
        return executeTasks(startIndex + maxConcurrent)
      }
    )
  }

  return executeTasks().then(() => results)
}

// Scenario
function createTask(id) {
  return () =>
    new Promise((resolve) => {
      setTimeout(() => {
        console.log(`API ${id} finished`)
        resolve(`Data from API ${id}`)
      }, Math.random() * 1000) // Random timeout to simulate different API response times
    })
}

let callApis = Array.from({ length: 100 }, (_, i) => createTask(i + 1))

throttleAsync(callApis, 5)
  .then((data) => {
    console.log('All data:', data)
  })
  .catch((err) => {
    console.error(err)
  })
```

---

**70. Find the first two numbers that sum up to 0**

```js
// Example Input

findTwo([1, 2, 3, -1])
// [0,3]

findTwo([1, 2, 3, -1, -2, 0])
// [0,3] or [1,4] or [5, 5]

findTwo([1, 2, 3, 4])
// null
```

```js
function findTwo(nums) {
  // Create a set to store numbers
  let numSet = new Set()

  for (let i = 0; i < nums.length; i++) {
    if (numSet.has(-nums[i])) {
      //nums[i] is -1 as per the iteration i=3, so -nums[i] at iteration 3 will be positive 3
      return [nums.indexOf(-nums[i]), i] //indexOf positive 3, indexOf iteration will be the returned output
    }
    // Add the current number to the set
    numSet.add(nums[i])
  }

  // If no such pair exists, return null
  return null
}

// Test cases
console.log(findTwo([1, 2, 3, -1])) // [0,3]
console.log(findTwo([1, 2, 3, -1, -2, 0])) // [0,3] (it may vary based on which pair is found first)
console.log(findTwo([1, 2, 3, 4])) // null
console.log(findTwo([0, 1, 0, 4])) // [0, 2]
```

---

**71. Find the largest difference**

```js
largestDiff([-1, 2, 3, 10, 9])
// 11,  obviously Math.abs(-1 - 10) is the largest

largestDiff([])
// 0

largestDiff([1])
// 0
```

```js
function largestDiff(nums) {
  // If the array has 0 or 1 elements, return 0
  if (nums.length <= 1) {
    return 0
  }

  // Find the max and min values in the array
  let max = Math.max(...nums)
  let min = Math.min(...nums)

  // Return the absolute difference between max and min
  return Math.abs(max - min)
}

// Test cases
console.log(largestDiff([-1, 2, 3, 17, 9])) // 18
console.log(largestDiff([])) // 0
console.log(largestDiff([1])) // 0
```

---

**72. Implement your own memoizeOne(), it takes 2 arguments**

- You might need to restrict the cache capacity, just like memoize-one , it only remembers the latest arguments and result.

Below are the two arguments:

1. target function
2. (optional) a equality check function to compare current and last arguments

Default equality check function should be a shallow comparison on array items with strict equal ===

---

**73. Implement classNames()**

```js
function classNames(...args) {
  //ex: ["class1", "class2"].flat
  const flattenedArgs = args.flat(Infinity) //is useful when array has nested arrays
  console.log('args.flat', flattenedArgs)
  console.log('args', args)
  return flattenedArgs
    .reduce((result, item) => {
      if (item === null) return result
      switch (typeof item) {
        case 'string':
        case 'number':
          result.push(item)
          break
        case 'object':
          for (let [key, value] of Object.entries(item)) {
            if (!!value) {
              result.push(key)
            }
          }
          break
      }

      return result
    }, [])
    .join(' ')
}

// Test cases
console.log(classNames('class1', 'class2')) // "class1 class2"
console.log(classNames('class1', { class2: true, class3: false })) // "class1 class2"
console.log(classNames('class1', { class2: true, class3: false }, 'class4')) // "class1 class2 class4"
console.log(classNames(['class1', 'class2', ['class3', 'class4']])) // "class1 class2 class3 class4"
```

---

**74. Implement \_.chunk()** - underscore.chunk()

```js
//Example: chunk splits array into groups with the specific size.
chunk([1, 2, 3, 4, 5], 1)
// [[1], [2], [3], [4], [5]]

chunk([1, 2, 3, 4, 5], 2)
// [[1, 2], [3, 4], [5]]

chunk([1, 2, 3, 4, 5], 3)
// [[1, 2, 3], [4, 5]]

chunk([1, 2, 3, 4, 5], 4)
// [[1, 2, 3, 4], [5]]

chunk([1, 2, 3, 4, 5], 5)
// [[1, 2, 3, 4, 5]]
```

---

**75.create your own Cookie**

```js
1. it should support get and set.
2. support max-age which means the cookie should be deleted after certain time(in seconds).
```

```js
//Examples:
document.myCookie = 'bfe=dev; max-age=1'
// "bfe=dev; max-age=1"

document.myCookie
// "bfe=dev"

// after 1 second
document.myCookie
// ""
```

```js
;(function () {
  let cookies = {}

  // Helper to parse cookie string
  function parseCookie(cookieStr) {
    let parts = cookieStr.split(';')
    let cookie = {}
    parts.forEach((part) => {
      let [key, value] = part.trim().split('=')
      cookie[key] = value
    })
    return cookie
  }

  // Custom property definition
  Object.defineProperty(document, 'myCookie', {
    get: function () {
      // Return all cookies as string, without max-age attribute
      return Object.entries(cookies)
        .filter(([key]) => key !== 'max-age')
        .map(([key, value]) => `${key}=${value}`)
        .join('; ')
    },
    set: function (value) {
      let newCookie = parseCookie(value)

      if (newCookie['max-age']) {
        let maxAge = parseInt(newCookie['max-age'], 10)
        setTimeout(() => {
          for (let key in newCookie) {
            if (cookies[key]) {
              delete cookies[key]
            }
          }
        }, maxAge * 1000)
        delete newCookie['max-age']
      }

      cookies = { ...cookies, ...newCookie }
    },
  })
})()

// Test
document.myCookie = 'bfe=dev; max-age=1'
console.log(document.myCookie) // "bfe=dev"
setTimeout(() => {
  console.log(
    'deleted the cookie as per the max-age setting',
    document.myCookie
  ) // ""
}, 1100)
```

---

**76.create a localStorage wrapper with expiration support**

```js
myLocalStorage.setItem('bfe', 'dev', 1000)
myLocalStorage.getItem('bfe')
// 'dev'

//after 1 second
myLocalStorage.getItem('bfe')
// null
```

**77.implement promisify()**

```js
// Let's take a look at following error-first callback.
const callback = (error, data) => {
  if (error) {
    // handle the error
  } else {
    // handle the data
  }
}

// Now think about async functions that takes above error-first callback as last argument.
const func = (arg1, arg2, callback) => {
  // some async logic
  if (hasError) {
    callback(someError)
  } else {
    callback(null, someData)
  }
}

// You see what needs to be done now. Please implement promisify() to make the code better.
const promisedFunc = promisify(func)

promisedFunc()
  .then((data) => {
    // handles data
  })
  .catch((error) => {
    // handles error
  })
```

**78. implement undefinedToNull() to return a copy that has all undefined replaced with null.**

```js
undefinedToNull({ a: undefined, b: 'BFE.dev' })
// {a: null, b: 'BFE.dev'}

undefinedToNull({ a: ['BFE.dev', undefined, 'bigfrontend.dev'] })
// {a: ['BFE.dev', null, 'bigfrontend.dev']}
```

```js
function undefinedToNull(obj) {
  // Base case: if the input is not an object, return it as-is.
  if (obj === null || typeof obj !== 'object') {
    return obj
  }

  // Handle arrays
  if (Array.isArray(obj)) {
    return obj.map((item) => undefinedToNull(item))
  }

  // Handle objects
  let result = {}
  for (let key in obj) {
    if (obj[key] === undefined) {
      result[key] = null
    } else {
      result[key] = undefinedToNull(obj[key])
    }
  }
  return result
}

// Test cases
console.log(undefinedToNull({ a: undefined, b: 'BFE.dev' }))
// {a: null, b: 'BFE.dev'}

console.log(undefinedToNull({ a: ['BFE.dev', undefined, 'bigfrontend.dev'] }))
// {a: ['BFE.dev', null, 'bigfrontend.dev']}
```

---

**79.merge identical API calls**

```js
//Suppose we have a utility function getAPI() which fetches data.

const getAPI = (path, config) => { ... }

const list1 = await getAPI('/list', { keyword: 'bfe'})
const list2 = await getAPI('/list', { keyword: 'dev'})
//It works great. Util the UI become so complicated that same API might be called for multiple time within a relatively short period of time.

//You want to avoid the unnecessary API calls, based on following assumption:

//GET API call response hardly changes within 1000ms.

//So identical GET API calls should return the same response within 1000ms. By identical, it means path and config are deeply equal.

//You create createGetAPIWithMerging(getAPI), which works like following.


const getAPIWithMerging = createGetAPIWithMerging(getAPI)

getAPIWithMerging('/list', { keyword: 'bfe'}).then(...)
// 1st call,  this will call getAPI

getAPIWithMerging('/list', { keyword: 'bfe'}).then(...)
// 2nd call is identical to 1st call,
// so getAPI is not called,
// it resolves when 1st call resolves

getAPIWithMerging('/list', { keyword: 'dev'}).then(...)
// 3rd call is not identical, so getAPI is called

// after 1000ms
getAPIWithMerging('/list', {keyword: 'bfe'}).then(...)
// 4th call is identical to 1st call,
// but since after 1000ms, getAPI is called.
Attention for memory leak!
Your cache system should not bloat. For this problem, you should have 5 cache entries at maximum, which means:

getAPIWithMerging('/list1', { keyword: 'bfe'}).then(...)
// 1st call, call callAPI(), add a cache entry
getAPIWithMerging('/list2', { keyword: 'bfe'}).then(...)
// 2nd call, call callAPI(), add a cache entry
getAPIWithMerging('/list3', { keyword: 'bfe'}).then(...)
// 3rd call, call callAPI(), add a cache entry
getAPIWithMerging('/list4', { keyword: 'bfe'}).then(...)
// 4th call, call callAPI(), add a cache entry
getAPIWithMerging('/list5', { keyword: 'bfe'}).then(...)
// 5th call, call callAPI(), add a cache entry

getAPIWithMerging('/list6', { keyword: 'bfe'}).then(...)
// 6th call, call callAPI(), add a cache entry
// cache of 1st call is removed

getAPIWithMerging('/list1', { keyword: 'bfe'}).then(...)
// identical with 1st call, but cache of 1st call is removed
// new cache of entry is added
clear()
//For test purpose, please provide a clear method to clear all cache.

getAPIWithMerging.clearCache()


```

---

**80. call APIs with pagination**

```js
// Have you ever met some APIs with pagination, and needed to recursively fetch them based on response of previous request ?

// Suppose we have a /list API, which returns an array items.

// fetchList is provided for you
const fetchList = (since?: number) =>
  Promise<{items: Array<{id: number}>}>

// for initial request, we just fetch fetchList. and get the last item id from response.
// for next page, we need to call fetchList(lastItemId).
// repeat above process.
// The /list API only gives us 5 items at a time, with server-side filtering, it might be less than 5. But if none returned, it means nothing to fetch any more and we should stop.
// You are asked to create a function that could return arbitrary amount of items.
```

```js
const fetchListWithAmount = async (amount = 5) => {
  const result = []

  while (result.length <= amount) {
    const lastItem = result[result.length - 1]
    //If it's the first iteration and there's no lastItem, it fetches from the beginning.
    const { items } = await fetchList(lastItem?.id)
    result.push(...items)
    if (!items.length) {
      break
    }
  }

  return result.slice(0, amount)
}
```

---

**81.can you shuffle() an array?**

---

**82. Sort given array of objects with age in JavaScript**

```js
// Input

const arr = [
  { name: 'Prathi', age: 32, place: 'Pune' },
  { name: 'Raj', age: 26, place: 'Mumbai' },
  { name: 'Arun', age: 28, place: 'Delhi' },
]
//Output: [26,28,32]
```

```js
const arr = [
  { name: 'Prathi', age: 32, place: 'Pune' },
  { name: 'Raj', age: 26, place: 'Mumbai' },
  { name: 'Arun', age: 28, place: 'Delhi' },
]

// Implement a basic bubble sort
for (let i = 0; i < arr.length; i++) {
  for (let j = 0; j < arr.length - 1 - i; j++) {
    if (arr[j].age > arr[j + 1].age) {
      const temp = arr[j]
      arr[j] = arr[j + 1]
      arr[j + 1] = temp
    }
  }
}

// Extract the ages to a separate array
const sortedAges = []
for (let i = 0; i < arr.length; i++) {
  sortedAges.push(arr[i].age)
}

console.log(sortedAges) // [26, 28, 32]
```

---

**83.find the max number from each string of array**

```js
// Input

const arr = ['23-43-65', '98-12-100', '12-23-239']
//Output: [65,100,239]
```

```js
const arr = ['23-43-65', '98-12-100', '12-23-239']

const result = arr.map((str) => {
  console.log('str', str) //ex: 23-43-65 in string format
  return Math.max(...str.split('-').map((num) => parseInt(num, 10)))
})

console.log(result) // [65, 100, 239]
```

---
