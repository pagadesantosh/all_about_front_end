## Throttling and Debouncing

**Throttling**

- A function doesn't get called often more than a specified interval, even if it's invoked multiple times.
- Ex: If you throttle a function to be called at most once every 300 ms, it will ignore any additional calls that happen before the 300 ms have passed.

```js
function updateLayout() {
  console.log('Updating layout...');
}

function throttle(func, limit) {
  //maintain a variable for mutation (ex: isThrottle = false)
  let isThrottle = false;
  // return another function with args
  return function (...args) {
    // check the variable is not true, if yes then mutate the variable to true,
    if (!isThrottle) {
      isThrottle = true;
      func.apply(this, args);
      setTimeout(() => {
        isThrottle = false;
      }, limit);
    }
  };
}

let isThrottled = throttle(updateLayout, 100);

window.addEventListener('resize', () => {
  isThrottled();
});
```

**Debouncing**

- A function doesn't get called until after a specified amount of time has passed since it was last invoked.

- Ex: execute this function only if 100 milliseconds have passed without it being called

```js
function searchQuery(query) {
  console.log(`Searching for: ${query}`);
}

function debounce(func, delay) {
  //maintain a variable (ex: timer)
  let timer;

  //return another function with args
  return function (...args) {
    clearTimeout(timer);
    //mutate that variable
    timer = setTimeout(() => {
      func.apply(this, args);
    }, delay);
  };
}

const debouncedSearch = debounce(searchQuery, 100);
let inputState = 'Hello';
debouncedSearch(inputState);
```
