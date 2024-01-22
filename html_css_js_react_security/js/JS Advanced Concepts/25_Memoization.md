### Memoization:

- In order to understand how Dynamic Programming works, we need to understand what caching means.
- Caching is a way to store values so you can use them later on.
- Memoization is a specific form of caching that we're going to be talking about because we use this a lot in Dynamic Programming.
- In simpler terms, Memoization is returning the cached value

```js
//normal func
function add80(n) {
  return n + 80;
}

add80(89);
```

```js
// memoized func

let cache = {};
const memoize = (n) => {
  if (n in cache) {
    return cache[n];
  } else {
    console.log('Takes Time');
    cache[n] = n + 80;
    return cache[n];
  }
};

console.log('1', memoize(5)); // Takes Time
console.log('2', memoize(5)); // Returns from the cache
```

### Caching Example using Closures

```js
const memoize = (n) => {
  let cache = {};
  return function (n) {
    if (n in cache) {
      return cache[n];
    } else {
      console.log('Takes Time');
      cache[n] = n + 80;
      return cache[n];
    }
  };
};

const memoized = memoize()
console.log(memoized(5))  // Takes Time
console.log(memoized(5)) // Returns from the cache
```
