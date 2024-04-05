## Proxy Pattern

- The Proxy Pattern is a fundamental design pattern that <ins>***provides a placeholder for another object to control access to it***</ins>. 
- This pattern is especially useful in situations where you want ***<ins>to add a layer of protection, logging, lazy initialization, or access control to the actual object without changing its code.***</ins>

```js
// Target object
function NetworkFetch(url) {
  this.url = url;
}

NetworkFetch.prototype.fetchData = function () {
  console.log(`Fetching data from ${this.url}...`);
  // Imagine an actual network request here
};

// Proxy object
function NetworkFetchProxy(url) {
  this.networkFetch = new NetworkFetch(url);
}

NetworkFetchProxy.prototype.fetchData = function () {
  console.log('Proxy: Checking access before fetching data.');
  // Perform additional actions or checks before the actual operation
  this.networkFetch.fetchData();
  // Perform additional actions or checks after the actual operation
  console.log('Proxy: Logging the time of request.');
};

// Usage
const proxy = new NetworkFetchProxy('http://example.com');
proxy.fetchData();


// Output:
// Proxy: Checking access before fetching data.
// Fetching data from http://example.com...
// Proxy: Logging the time of request.
```
----

### ES6 Proxy Version


```js
// Target object
function NetworkFetch(url) {
    this.url = url;
}

NetworkFetch.prototype.fetchData = function() {
    console.log(`Fetching data from ${this.url}...`);
    // Imagine an actual network request here
};

// Proxy handler
const handler = {
    get(target, prop, receiver) {
        const originalMethod = target[prop];
        if (typeof originalMethod === 'function') {
            return function(...args) {
                console.log('Proxy: Checking access before fetching data.');
                // Perform additional actions or checks before the actual operation
                const result = originalMethod.apply(target, args);
                // Perform additional actions or checks after the actual operation
                console.log('Proxy: Logging the time of request.');
                return result;
            };
        }
        return originalMethod;
    }
};

// Creating a proxy
const networkFetch = new NetworkFetch('http://example.com');
const proxy = new Proxy(networkFetch, handler);

// Usage
proxy.fetchData();

// Output:
// Proxy: Checking access before fetching data.
// Fetching data from http://example.com...
// Proxy: Logging the time of request.
```

- In the ES6 version, we use the Proxy constructor to create a proxy around the NetworkFetch instance. 
- The handler object defines traps for interactions with the proxy. 
- Here, the get trap intercepts method calls and allows us to inject additional behavior before and after the method invocation. This approach is more dynamic and can easily be applied to various objects without creating specific proxy classes for each.