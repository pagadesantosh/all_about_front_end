- useCallback hook was introduced in React to memoize callbacks.
- The problem with callbacks in React <strong><u>that functions are recreated every time when a component is re-rendered</strong></u> eve though they have the same logic.

```js
import React, { useState } from "react";

const Avocado = () => {
  const [count, setCount] = useState(0);

  const addAvocado = () => {
    setCount(count + 1);
  };

  return (
    <>
      <Addvocado add={addAvocado} />
      <div>{Array(count).fill("🥑").join(",")}</div>
    </>
  );
};

// Another component

const Addvocado = ({ add }) => {
  console.log("component re-rendered");
  return (
    <>
      <button onClick={add}>Add avocado</button>
    </>
  );
};
```

##### Everytime we click the button, the button gets re-rendered even though no state or visual changes are happening for the Addvocado component

```js
const avocados01 = () => ["🥑", "🥑", "🥑"];
const avocados02 = () => ["🥑", "🥑", "🥑"];

avocados01 === avocados02; // returns false
avocados01 === avocados01; // returns true
```

##### This is because whenever we create a new function we create a new instance and they never be same.

#### Here Memoizing callbacks comes into picture. <u>By always returning the same function we can prevent un-necessary re-renders</u>

- We need to fix the component to make it only render the button once. To fix this, <u>we need to wrap the inline function with the useCallback hook like below:</u>

```js
import React, { useState } from "react";

const Avocado = () => {
  const [count, setCount] = useState(0);

  // const addAvocado = () => {
  //   setCount(count + 1);
  // };

  const memoizedAddAvocado = useCallback(() => {
    setCount((c) => c + 1);
  }, [setCount]);

  return (
    <>
      <Addvocado add={memoizedAddAvocado} />
      <div>{Array(count).fill("🥑").join(",")}</div>
    </>
  );
};

// Wrapping our Another component with React.memo

const Addvocado = React.memo(({ add }) => {
  console.log("component re-rendered");
  return (
    <>
      <button onClick={add}>Add avocado</button>
    </>
  );
});
```
