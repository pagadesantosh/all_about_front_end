### React HOC Pattern (Higher Order Component)

#### What is HOC ?

- Higher Order Component receives a component, applies a certain logic and then return that component with those additional logics

#### When to use HOC?

- When we want to apply same logic to multiple components

```js
//App.jsx

import './styles.css';
import Comp1 from './Comp1';
import Comp2 from './Comp2';

export default function App() {
  return (
    <div className='App'>
      <Comp1 />
      <Comp2 />
    </div>
  );
}
```

```js
// Comp1.js
import { forwardRef } from 'react';
import WithDimension from './WithDimension';
const Comp1 = (props, ref) => {
  return (
    <div ref={ref} className='comp1'>
      Hey I am comp1 width: {props.width}
    </div>
  );
};

export default WithDimension(forwardRef(Comp1));
```

```js
// Comp2.js
import { forwardRef } from 'react';
import WithDimension from './WithDimension';
const Comp2 = (props, ref) => {
  return (
    <div ref={ref} className='comp2'>
      Hey I am comp2 width: {props.width}
    </div>
  );
};

export default WithDimension(forwardRef(Comp2));
```

```js
// WithDimension.js

import { useEffect, useRef, useState } from 'react';

const withDimension = (Element) => {
  function WithDimensions(props) {
    const compRef = useRef();
    const [width, setWidth] = useState(null);
    const [height, setHeight] = useState(null);

    useEffect(() => {
      if (compRef.current) {
        setWidth(compRef.current.offsetWidth);
        setHeight(compRef.current.offsetHeight);
      }
    }, [compRef]);
    return <Element ref={compRef} width={width} height={height} {...props} />;
  }
  return WithDimensions;
};

export default withDimension;
```

```js
img {
  height: 100px;
  display: block;
  margin-bottom: 10px;
}
.comp1 {
  height: 100px;
  width: 200px;
}

.comp2 {
  height: 150px;
  width: 250px;
}
 
```
