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
  let cookies = {};

  // Helper to parse cookie string
  function parseCookie(cookieStr) {
    let parts = cookieStr.split(';');
    let cookie = {};
    parts.forEach((part) => {
      let [key, value] = part.trim().split('=');
      cookie[key] = value;
    });
    return cookie;
  }

  // Custom property definition
  Object.defineProperty(document, 'myCookie', {
    get: function () {
      // Return all cookies as string, without max-age attribute
      return Object.entries(cookies)
        .filter(([key]) => key !== 'max-age')
        .map(([key, value]) => `${key}=${value}`)
        .join('; ');
    },
    set: function (value) {
      let newCookie = parseCookie(value);

      if (newCookie['max-age']) {
        let maxAge = parseInt(newCookie['max-age'], 10);
        setTimeout(() => {
          for (let key in newCookie) {
            if (cookies[key]) {
              delete cookies[key];
            }
          }
        }, maxAge * 1000);
        delete newCookie['max-age'];
      }

      cookies = { ...cookies, ...newCookie };
    },
  });
})();

// Test
document.myCookie = 'bfe=dev; max-age=1';
console.log(document.myCookie); // "bfe=dev"
setTimeout(() => {
  console.log(
    'deleted the cookie as per the max-age setting',
    document.myCookie
  ); // ""
}, 1100);
```
