1. Types of functions in JS(Regular, function expressions, arrow functions)

2. Arrow functions this keyword context with example
3. Why do we use React over other frameworks(explain about virtual dom and other advantages)
4. class and functional components ((Which do you prefer and why))

5. what is props drilling, how to overcome the issue (context with example), why do we use it and syntax for creating and using context
6.  How do you handle list rendering in React while using JSX?
7.  If a parent component have two children, how to re-render only 1 children
8.  What are real dom and shadow dom
9.  Scenario based question on parent child rendering and how to optimize it
-------
### 10. how to manage state globally without using redux (useContext and useReducer)

#### Step 1: Define Your Context
```js
import React, { createContext, useReducer } from 'react';

// Initial state
const initialState = {
  count: 0,
};

// Create context
const GlobalContext = createContext(initialState);

// Reducer function
const reducer = (state, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { ...state, count: state.count + 1 };
    case 'DECREMENT':
      return { ...state, count: state.count - 1 };
    default:
      return state;
  }
};

// Context Provider component
const GlobalProvider = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <GlobalContext.Provider value={{ state, dispatch }}>
      {children}
    </GlobalContext.Provider>
  );
};

export { GlobalContext, GlobalProvider };
```

#### Step 2: Create a Component to Use the Global State
```js
import React, { useContext } from 'react';
import { GlobalContext } from './GlobalState';

const Counter = () => {
  const { state, dispatch } = useContext(GlobalContext);

  return (
    <div>
      <h1>Count: {state.count}</h1>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'DECREMENT' })}>Decrement</button>
    </div>
  );
};

export default Counter;
```

#### Step 3: Set Up Your App Component
```js
import React from 'react';
import { GlobalProvider } from './GlobalState';
import Counter from './Counter';

function App() {
  return (
    <GlobalProvider>
      <div>
        <h1>Welcome to the Counter App</h1>
        <Counter />
      </div>
    </GlobalProvider>
  );
}

export default App;
```
----

11. MicroFrontend using module federation, How the shell will render the MFE
   - past experience with Micro-frontend and how you used to pass data between MFE's
   - questions on designing and how you divide a website into different components and why
   - if you want develop your company website using MFE how many MFE will you create and why?
   - how to optimize the loading time of an MFE

-----

### 12. As redux is third party library which will take time to load compared to context(as it is built in). why you choose redux why not context

#### 1. Performance and Optimization
- **Redux**: 
  - `Optimized` for frequent updates and complex state interactions across large applications. 
  - Redux **uses a single immutable state tree**, which can be more efficient at scale because components subscribe only to the parts of the state they need. 
  - This <ins>**minimizes unnecessary re-renders**</ins>.
<br/>

- **Context API**: 
  - Suitable **for simpler or medium-scale applications**, but it can lead to performance bottlenecks in larger apps. 
  - When a context value changes, **<ins>all components consuming that context will re-render, regardless of whether the change affects them**</ins>.


#### 2. Middleware and Enhancements
- **Redux**: 
  - Supports middleware, allowing for features like `logging`, `crash reporting`, performing asynchronous tasks, and more. 
  - Middleware like `Redux Thunk` and `Redux Saga` can <ins>**handle side effects</ins> in a more manageable way**.
<br/>

- **Context API**: 
   - `Lacks` built-in middleware support, **making it less suitable for complex** asynchronous logic or other middleware-driven enhancements unless supplemented by additional libraries or custom code.
#### 3. Developer Tools and Ecosystem
- **Redux**: 
  - Has a robust set of tools, most notably the **Redux DevTools**, which allow developers 
  - to track every state change, 
  - travel through time by inspecting each action, 
  - and re-evaluate state. 
<br/>

- **Context API**: 
  - While it's simpler and integrated directly into React, it **doesn’t** have a comparable set of tools **for debugging** and `lacks` the extensive ecosystem of libraries and plugins available for Redux.

#### 4. Community and Resources
- **Redux**: 
  - Benefits from a large community and a wealth of resources, including tutorials, best practice guides, and third-party libraries. 
  - This can accelerate development and troubleshooting.
<br/>

- **Context API**:  
  - Although well-documented in the React docs, the patterns and practices around Context **are less standardized than Redux**, which can lead to inconsistent implementations across different projects.

#### 5. Predictability and Structure
- **Redux**: 
   - Enforces strict patterns and workflows, such as defining reducers and actions, which can help in maintaining a large codebase at scale. 
   - It **provides** a <ins>more predictable state management model</ins> through controlled updates.
<br/>
  
- **Context API**:  
   - Offers more flexibility, but without the enforced structure of Redux, which can lead to varied implementations and **potentially less predictable code.**
  
#### 6. Scalability
- **Redux**: 
   - Its architecture and ecosystem are <ins>**designed to scale smoothly as the application grows**</ins>. 
   - This makes it a <ins>**preferred choice</ins> for enterprise-level applications**.
<br/>
  
- **Context API**:  
   - **Best for smaller applications** or specific areas within an app where global state is overkill. Scaling can introduce performance issues as the number of context consumers grows.

#### Conclusion
- For `small` to `medium-sized` applications, especially those built as part of learning projects or **where the state is relatively straightforward**, ***React's Context API*** might be <ins>**more than sufficient**</ins> and easier to integrate. 
- However, for **`large-scale` applications with `complex state` interactions**, frequent updates, and a need for fine-grained performance optimizations, `Redux` or similar state management libraries <ins>**remain a strong choice**</ins> despite the initial overhead. 


----
13. testing frameworks (asked about RTL)
