## undefinedToNull

```js
function undefinedToNull(arg) {
  // anything that is primitives (ex: strings, numbers, boolean)
  if (typeof arg !== 'object' || arg === null) {
    return arg ?? null;
  }

  //Ex: key is a, value is undefined
  for (const [key, value] of Object.entries(arg)) {
    if (value === undefined) {
      //mutate the key with null
      arg[key] = null;
    } else {
      //recursively call the same function and this will execute the primitives logic of first if condition
      arg[key] = undefinedToNull(value);
    }
  }

  return arg;
}

console.log(undefinedToNull({ a: undefined, b: 'BFE.dev' }));
// {a: null, b: 'BFE.dev'}

console.log(undefinedToNull({ a: ['BFE.dev', undefined, 'bigfrontend.dev'] }));
// {a: ['BFE.dev', null, 'bigfrontend.dev']}
```
