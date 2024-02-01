### Create your own cookie

```js
1. it should support get and set.
2. support max-age which means the cookie should be deleted after certain time(in seconds).
```

```js
//Examples:
document.myCookie = 'bfe=dev; max-age=1';
// "bfe=dev; max-age=1"

document.myCookie;
// "bfe=dev"

// after 1 second
document.myCookie;
// ""
```

```js
// Solution

(function () {
  // Helper function to parse cookie string
  function parseCookieString(cookieStr) {
    let cookies = {};
    let parts = cookieStr.split(';');
    parts.forEach((part) => {
      let [key, value] = part.trim().split('=');
      cookies[key] = decodeURIComponent(value);
    });
    return cookies;
  }

  // Custom property definition
  Object.defineProperty(document, 'myCookie', {
    get: function () {
      // Read all cookies from document.cookie
      return parseCookieString(document.cookie);
    },
    set: function (value) {
      // Set cookie using document.cookie
      document.cookie = value;
    },
  });
})();

// Test
document.myCookie = 'bfe=dev; max-age=5'; // Set a cookie with max-age of 5 seconds
console.log(document.myCookie); // Should show the cookie "bfe=dev"

// After 8 seconds, the cookie should be expired and no longer visible
setTimeout(() => {
  console.log('After expiration:', document.myCookie); // Should show an empty object or no 'bfe' cookie
}, 8000);
```
