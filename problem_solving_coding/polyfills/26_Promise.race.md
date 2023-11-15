## Promise.race()

**Definition**: takes an iterable of promises and returns the first resolved/rejected (returns a single promise)

```js
//syntax:
Promise.race(iterable);
```

<strong>Approach Taken:</strong>

1. promise.customRace is a function that takes array of promises (param)
2. this function return new Promise(resolve, reject) and then start writing the logic as follows
3. write a for of loop ex: for(let singlePromiseItem of promisesArray)
4. Promise.resolve(singlePromiseItem).then(resolve, reject)

```js
if (typeof Promise.customRace !== 'function') {
  Promise.customRace = function (promises) {
    return new Promise((resolve, reject) => {
      // Ensure the input is iterable
      if (!Array.isArray(promises)) {
        throw new TypeError(
          'The arguments to Promise.customRace must be an iterable'
        );
      }

      // Resolve or reject the main promise as soon as one of the input promises settles
      for (let p of promises) {
        Promise.resolve(p).then(resolve, reject);
      }
    });
  };
}

// Example Usage
function processLocally(data) {
  return new Promise((resolve) => {
    // Simulated delay for local processing
    setTimeout(() => resolve(`Local result for ${data} 1000ms`), 1000);
  });
}

function processRemotely(data) {
  return new Promise((resolve) => {
    // Simulated delay for remote processing
    setTimeout(() => resolve(`Remote result for ${data} 500ms`), 500);
  });
}

const data = 'sampleTask';
Promise.customRace([processLocally(data), processRemotely(data)])
  .then((result) => console.log(result)) // Outputs: "Remote result for sampleTask 500ms"
  .catch((error) => console.error(error));
```
