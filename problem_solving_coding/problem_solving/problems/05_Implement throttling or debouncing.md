## Throttling and Debouncing

**Throttling**

- A function doesn't get called often more than a specified interval, even if it's invoked multiple times.
- Ex: If you throttle a function to be called at most once every 300 ms, it will ignore any additional calls that happen before the 300 ms have passed.

```js
const throttle = (func, limit) => {
  let inThrottle;
  return (...args) => {
    if (!inThrottle) {
      func(...args);
      inThrottle = true;
      setTimeout(() => (inThrottle = false), limit);
    }
  };
};

// Usage:
const throttledFunction = throttle(() => console.log('Throttled!'), 300);
```

**Debouncing**

- A function doesn't get called until after a specified amount of time has passed since it was last invoked.

- Ex: execute this function only if 100 milliseconds have passed without it being called

```js
const debounceFunc = (func, delay) => {
  let timer;
  return function (...args) {
    const context = this;
    clearTimeOut(timer);
    timer = setTimeOut(() => {
      func.apply(context, args);
    }, delay);
  };
};

// Usage:
const debouncedFunction = debounce(() => console.log('Debounced!'), 300);
```
