### Implement LRU Cache

**Approach Taken**:

1. at first we will use put to add key/value pairs in the Cache Map. (Ex: cache: {1: 1, 2: 2})
2. then when we try to get(key), it runs `const value = cache.get(key)` logic
3. we then delete that key from the cache and add key value pair again (this makes the cache to look like {2: 2, 1: 1})
4. we then return the value of the get function
5. now when we try to put another key/value pair in the Cache Map. It satisfies the `cache.size === capacity` condition
6. So, we need to grab the first key from the cache object, this can be done using cache.keys().next().value,
7. Then delete that key
8. outside to all these if/elseif conditions, we have to write our core logic `cache.set(key,value)`

```js
function createLRUCache(capacity) {
  let cache = new Map();

  function get(key) {
    if (!cache.has(key)) {
      return -1;
    }
    const value = cache.get(key);
    cache.delete(key);
    cache.set(key, value);
    return value;
  }

  function put(key, value) {
    if (cache.has(key)) {
      cache.delete(key);
    } else if (cache.size === capacity) {
      const firstKey = cache.keys().next().value;
      cache.delete(firstKey);
    }
    cache.set(key, value);
  }

  return { get, put };
}

// Usage example
const lruCache = createLRUCache(2);
lruCache.put(1, 1);
lruCache.put(2, 2);
console.log(lruCache.get(1)); // returns 1
lruCache.put(3, 3); // evicts key 2
console.log(lruCache.get(2)); // returns -1 (not found)
```
