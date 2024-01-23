### LocalStorage with Expiration

**_Approach Taken:_**

- maintain a timeouts object to store keys
- function returns an object, in this object we have 4 methods (getItem, setItem, removeItem, clear)
- getItem(key) simply use the window.localStorage.getItem(key), if this true then JSON.parse(item)
- removeItem(key) simply checks if timeouts[key] is true, if yes then clearTimeout(timeouts[key]) and delete timeouts[key]. also write the core logic of this (window.localStorage.removeItem(key))
- clear() method, does a loop based on the Object.keys(timeoutsObj).forEach((key)=>{
  clearTimeout(timeouts[key])
  })
  timeouts = {}
  window.localStorage.clear()
- core logic is setItem

```js
const MyLocalStorage = (function () {
  let timeouts = {};

  return {
    getItem(key) {
      const item = window.localStorage.getItem(key);
      return item ? JSON.parse(item) : null;
    },

    setItem(key, value, maxAge) {
      if (typeof maxAge !== 'number') {
        throw new Error('maxAge must be a number');
      }

      window.localStorage.setItem(key, JSON.stringify(value));

      if (timeouts[key]) {
        clearTimeout(timeouts[key]);
      }

      if (maxAge > 0) {
        // it sets a timer to automatically remove the item from local storage after the specified duration.
        timeouts[key] = setTimeout(() => {
          window.localStorage.removeItem(key);
          // This removes the reference to the timeout from the timeouts object.
          // It's a cleanup step to prevent memory leaks and to ensure that the timeouts object doesn't hold unnecessary references.
          delete timeouts[key];
        }, maxAge);
      } else if (maxAge === 0) {
        // immediately removes the item from local storage.
        window.localStorage.removeItem(key);
      }
    },

    removeItem(key) {
      if (timeouts[key]) {
        clearTimeout(timeouts[key]);
        // This removes the reference to the timeout from the timeouts object.
        // It's a cleanup step to prevent memory leaks and to ensure that the timeouts object doesn't hold unnecessary references.
        delete timeouts[key];
      }
      window.localStorage.removeItem(key);
    },

    clear() {
      Object.keys(timeouts).forEach((key) => {
        clearTimeout(timeouts[key]);
      });
      timeouts = {};
      window.localStorage.clear();
    },
  };
})();

window.myLocalStorage = MyLocalStorage;

window.myLocalStorage.setItem('testKey', 'testValue', 10000); // Expires in 5000 milliseconds (5 seconds)
``;
console.log(window.myLocalStorage.getItem('testKey')); // Should log 'testValue'
```
