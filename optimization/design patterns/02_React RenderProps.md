### A `prop in a component` which is a `function and that returns JSX`

**Uses**:

- When we want to make the component customizable
- Provide ability to theme the component according to their design system

```js
//App.js

import './styles.css';
import Input from './Input';
export default function App() {
  const showValue = (value) => <b>The value is {value}</b>;
  const multiplyByTen = (value) => <>The multiplied value is {value * 10}</>;
  return (
    <div className='App'>
      <Input renderTextBelow={showValue} />
      <br />
      <Input renderTextBelow={multiplyByTen} />
    </div>
  );
}
```

```js
// Input.js

import { useState } from 'react';

const Input = (props) => {
  const [value, setValue] = useState(null);
  const handleChange = (e) => {
    setValue(e.target.value);
  };
  return (
    <>
      <input value={value} onChange={handleChange} />
      <br />
      {props.renderTextBelow(value)}
    </>
  );
};

export default Input;
```
