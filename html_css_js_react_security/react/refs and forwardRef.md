### Refs in React

- Refs in React are a feature that **_provides a way to access React DOM nodes or React elements directly_**.

- used in situations **_where you need to directly interact with an element for things that can't be done declaratively_** (i.e., through React's state and props system)

- <u>**Accessing DOM Nodes:**</u>

  - This is useful for **_managing focus_**, **_text selection_**, **_media playback_**, **_triggering imperative animations_**, and integrating with third-party DOM libraries.

- **useRef Hook:**
  - In functional components, the useRef hook serves the same purpose. It **_persists refs across renders_** and **_does not trigger a re-render when the ref changes_**.

```js
import React, { useRef } from 'react';

function MyComponent() {
  const myRef = useRef(null);

  return <div ref={myRef} />;
}
```

---

### Forwarding Refs

- Ref forwarding is a technique for automatically **passing a ref through a component to one of its children**.
- React also provides a way to forward refs through components to their children, **allowing components to give their parents access** to their DOM nodes.

#### How Ref Forwarding Works?

**1. Creating a Ref**: In the parent component, you create a ref using useRef hook.

**2. Passing the Ref to a Child:**: You pass this ref <u>**_down to a child component as a prop_**.</u>

**3. Forwarding the Ref in the Child Component:** The child component uses the React.forwardRef function <u>**_to forward this ref to a particular DOM element_**</u>

**4. Accessing the Ref in the Parent Component:**
The <u>**_parent component can then interact with the DOM node_**</u> or component instance <u>**_referenced by the ref as if it were directly part of the parent_**.</u>

```js
import React, { useRef, useEffect } from 'react';

// Child component using forwardRef
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className='FancyButton'>
    {props.children}
  </button>
));

// Parent component as a functional component
const App = () => {
  const buttonRef = useRef(null);

  useEffect(() => {
    // Equivalent to componentDidMount in class components
    if (buttonRef.current) {
      buttonRef.current.focus();
    }
  }, []); // Empty dependency array means this runs once after initial render

  return <FancyButton ref={buttonRef}>Click me!</FancyButton>;
};

export default App;
```

<u>**Note**</u>:
The FancyButton component forwards the ref to the button element, allowing the parent component (App) to interact with the button DOM node.
