### 1. Strengths and weakness as a developer

<details>

#### Strengths:
   - Expertise in Modern Frameworks:
   - Proficiency in Performance Optimization:
   - Responsive and Adaptive Design Skills
   - Cross-Browser Development:
   - Version Control and Team Collaboration

#### Weaknesses:
- Keeping Up with Rapid Changes
- Overemphasis on Code Perfection
- Balancing User Experience with Aesthetic Design
- Performance Debugging
<summary>
View Answer
</summary>
</details>

-----

### 2. Ecommerce site that has different components(header/footer/left nav/ right content) developed in different frameworks(react/angular/vue)
   - How will you design/develop
   - How can you communicate between the components
   - How can you use a common components(like a button) across different frameworks

<details>

### Design/Development:

1. **Micro Frontends Approach**: 
   - Utilize the micro frontends architecture, where each main component (header, footer, navigation, content) is developed and deployed as an independent application. 
   - This allows teams to work on each section using the most suitable framework for that component's needs.

2. **Web Components**: 
   - Implement Web Components for parts of the UI that are framework-agnostic. 
   - This encapsulates the styling and functionality, making them reusable across different frameworks.


3. **Module Federation or Iframes**: 
   - Tools like <ins>***Webpack's Module Federation can be used***</ins> to dynamically load separate components, even if they are built with different frameworks. 
   - Iframes can also be used as a last resort, but they are less favored due to performance and design limitations.

### Communication Between Components:

   1. **Custom Events**: 
      - For communication between components, custom events can be a viable option. When an action occurs in one component, it can dispatch an event that other components can listen for and react to.
   2. **Shared Global Store**: 
      - Implementing a global state management system like Redux or Vuex, or even the Context API in React, can provide a centralized store that is accessible to components regardless of the framework.
   3. **URL and Query Parameters:**
      - For simple state synchronization between components, URL and query parameters can be utilized, especially for navigation and content components that may rely on URL changes.


### Common Components Across Frameworks:

   1. **Build as Web Components**: 
      - Creating common UI elements like buttons as Web Components is one of the most effective methods to ensure compatibility across different frameworks. 
      - Web Components are based on web standards and can be integrated into React, Angular, Vue, or any other framework.
   2. **Use a Design System**: 
      - Implement a design system with a set of standards for design and code that includes common components. 
      - Tools like Storybook can be utilized to maintain this system and ensure that components have a consistent look and feel, as well as similar APIs across different frameworks.
   3. **CSS-in-JS Libraries**: 
      - Use CSS-in-JS libraries to style components. This can help in keeping a consistent style across components regardless of the framework, although it requires agreement on the library to be used across teams.
<summary>
View Answer
</summary>
</details>


----
   
### 3. What are the different module systems

<details>

-  in JavaScript, a module system is a <ins>***mechanism that allows you to split your code into separate units, or modules, each with its own scope***</ins>, and then include them as needed. 
-  This approach enhances code organization, maintainability, and reusability. 

<ins>**CommonJS (CJS)**:</ins> 
   - Used mainly in Node.js for server-side development. 
   - It ***allows for synchronous loading*** of modules. 
   - Modules are **loaded using `require()`** and **exported using `module.exports`**.

<ins>**Asynchronous Module Definition (AMD):**</ins>

   - Used for ***asynchronous module loading***, suitable for browsers. 
   - It's implemented by libraries like `RequireJS`. 
   - Modules are defined using `define()` and dependencies are loaded asynchronously.


<ins>**Universal Module Definition (UMD):**</ins>

- Aims to provide compatibility with both CommonJS and AMD as well as with the traditional global variable method. 
- It checks the environment and adapts accordingly, allowing the module to be used in different contexts.

<ins>**ES Modules (ESM):**</ins>
  -  The standard module system in modern JavaScript, introduced with ES6 (ECMAScript 2015). 
  -  It supports static analysis and tree-shaking for more efficient bundling. Modules are imported using the `import` keyword and exported using `export`.
<summary>
View Answer
</summary>
</details>



----

### 4. Unit testing - difference between mock/stub/spy


<details>

#### Mock:
- A mock is used to <ins>***verify interactions between methods***</ins> and ***integrates rules about how they are supposed to be called***. 
- <ins>**It can be set up with expectations**:</ins> methods that should be called, the order of calls, the parameters they are called with, etc. 
- If the expectations are **not** met, the mock will typically cause the test to **fail**.
- Useful in scenarios <ins>***where the interaction itself is what needs to be tested***</ins>, not just the output.


```js
// FUNCTION TO TEST
// logger.js
function logIfTrue(value) {
  if (value) {
    console.log('Value is true!');
  }
}
```

```js
// TEST USING A MOCK:
// logger.test.js
import { logIfTrue } from './logger';

test('should log message when value is true', () => {
  // Spy on console.log
  const logMock = jest.spyOn(console, 'log');
  logMock.mockImplementation(() => {});

  logIfTrue(true);

  expect(logMock).toHaveBeenCalledWith('Value is true!');
  logMock.mockRestore(); // Restore the original implementation
});
```
----

#### Stub:
- Stubs primarily ***serve to provide <ins>predefined responses to function calls***</ins> that are necessary for the unit test to run. 
- They typically <ins>***don't record information about calls***</ins>.
- Useful in scenarios where you just need <ins>***to make sure that a piece of code can handle the input and produce the correct output***</ins> without really caring about the interaction with the dependency
  
```js
// FUNCTION TO TEST
// user.js
async function getUser(id) {
  return fetch(`https://api.example.com/users/${id}`)
    .then(response => response.json());
}
```

```js
// TEST USING A STUB
// user.test.js
import { getUser } from './user';

// Jest allows us to mock functions in this way
jest.mock('node-fetch', () => jest.fn());

const fetch = require('node-fetch');

test('should return user data', async () => {
  const fakeUser = { id: 1, name: 'Saiteja Gatadi' };
  fetch.mockImplementation(() => Promise.resolve({
    json: () => Promise.resolve(fakeUser)
  }));

  const userData = await getUser(1);
  expect(userData).toEqual(fakeUser);
});
```
----

#### Spy:
- A spy <ins>***records some information based on how its methods were called***</ins>.
- This can <ins>***include tracking how many times methods were called, with what arguments they were called***</ins>, and so forth. 
- Unlike mocks, spies generally **do not allow you to set expectations before the code runs**; they record information about interactions to be asserted later.

```js
// FUNCTION TO TEST
// calculator.js
class Calculator {
  add(a, b) {
    return a + b;
  }
}
```

```js
// TEST USING A SPY:
// calculator.test.js
import Calculator from './calculator';

test('should call add method correctly', () => {
  const calc = new Calculator();
  const spy = jest.spyOn(calc, 'add');
  const result = calc.add(2, 3);

  expect(spy).toHaveBeenCalledWith(2, 3);
  expect(result).toBe(5);
  spy.mockRestore(); // Restore original method
});
```
----

### Summary
- **Stub**: Provides ***predefined responses***, doesn’t record anything.
- **Mock**: <ins>***Set up with expectations beforehand***</ins>, and the test fails if the expectations aren't met.
- **Spy**: Similar to a stub but also ***records information about how it was called***, which can be checked after the test execution.

<summary>
View Answer
</summary>
</details>

----

### 5. State management 

<details>

- React has its **built-in** state management capabilities, but as applications grow in complexity, developers often turn to **external libraries** to simplify and enhance the process.

#### 1. Local State Management (useState):

```js
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
---

#### 2. Lifting state up:

- When **multiple** components need to share and modify the **same state**, you can lift the state up to their **closest common ancestor**.

```js
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <ChildComponent count={count} setCount={setCount} />
      <AnotherChild count={count} />
    </>
  );
}

function ChildComponent({ count, setCount }) {
  return (
    <button onClick={() => setCount(count + 1)}>
      Increment
    </button>
  );
}

function AnotherChild({ count }) {
  return <p>Count: {count}</p>;
}
```
----

#### 3. Context API:

- For more global state needs, React **provides** the Context API, which allows you to share values across the entire component tree **without having to explicitly pass props** at every level.

```js
import React, { createContext, useContext, useState } from 'react';

const CountContext = createContext();

function CounterProvider({ children }) {
  const [count, setCount] = useState(0);
  const value = { count, setCount };
  
  return (
    <CountContext.Provider value={value}>
      {children}
    </CountContext.Provider>
  );
}

function App() {
  return (
    <CounterProvider>
      <ChildComponent />
      <AnotherChild />
    </CounterProvider>
  );
}

function ChildComponent() {
  const { count, setCount } = useContext(CountContext);
  return (
    <button onClick={() => setCount(count + 1)}>
      Increment
    </button>
  );
}

function AnotherChild() {
  const { count } = useContext(CountContext);
  return <p>Count: {count}</p>;
}
```
----


#### 4. External State Management Libraries

- **Redux**: 
  - provides a predictable state container for JavaScript apps. 
  - It helps you manage state globally and keep changes predictable and traceable

- **MobX**:
  - offers a more **flexible approach** to state management based on observable state objects. 
  - It is particularly useful for **complex states with many interdependencies**.

- **Recoil**:
   - developed by Facebook that provides several capabilities similar to Redux but with a simpler API and better integration with React's own capabilities.

- **Zustand**:
   - A minimalistic state management solution that uses hooks to provide a straightforward and intuitive way to manage global state across your app

<summary>
View Answer
</summary>
</details>

-----

### 6. Explain Redux flow, 
   - how to handle async actions, 
   - code example with 2 parents one child, 
   - how store updates the values, 
   - redux middleware

<details>


#### The Redux flow follows a strict unidirectional pattern:

1. **Action**: 
      - Actions are `payloads` of information that **send data from your application to your Redux store**. 
      - They are the <ins>***only source of information for the store***.</ins> 
      - You send them to the store using `store.dispatch()`.
<br/>

2. **Reducer**: 
   - Reducers specify <ins>***how the application's state changes in response to actions sent to the store***</ins>. 
   - Remember that reducers **are pure functions** that take the previous state and an action, and return the next state.
<br/>

3. **Store**: The `store` brings actions and reducers together. The store has the following responsibilities:

   - Holds application state;
   - Allows access to state via getState();
   - Allows state to be updated via dispatch(action);
   - Registers listeners via subscribe(listener);
   - Handles un-registering of listeners via the function returned by subscribe(listener).
<br/>

#### <ins>Handling Async Actions:</ins>

Redux by itself handles only synchronous actions. To work with asynchronous operations (like API requests), you need to use middleware such as redux-thunk or redux-saga.


- `Redux-Thunk` allows you to write <ins>**action creators that return a function**</ins> instead of an `action`. 
  - The thunk can be used to delay the dispatch of an action, or to dispatch only if a certain condition is met.


#### Example with Redux-Thunk:
- a simple example involving **two parent** components and **one child** component, using `Redux` for state management and `Redux-Thunk` for asynchronous actions.

<ins>**Setup**:</ins>

- Parent1 and Parent2 both display data.
- Child updates the data asynchronously.

```js
// actions.js
export const fetchDataSuccess = data => ({
  type: 'FETCH_DATA_SUCCESS',
  payload: data
});

export const fetchData = () => {
  return dispatch => {
    fetch('/some-api')
      .then(response => response.json())
      .then(data => dispatch(fetchDataSuccess(data)))
      .catch(error => console.error('Fetching data failed', error));
  };
};
```


```js
// reducer.js
const initialState = {
  data: null
};

function appReducer(state = initialState, action) {
  switch (action.type) {
    case 'FETCH_DATA_SUCCESS':
      return { ...state, data: action.payload };
    default:
      return state;
  }
}

export default appReducer;
```

```js
// store.js
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import appReducer from './reducer';

const store = createStore(
  appReducer,
  applyMiddleware(thunk)
);

export default store;
```
```js
// Parent1.js
import React from 'react';
import { useSelector } from 'react-redux';

function Parent1() {
  const data = useSelector(state => state.data);
  return <div>Data in Parent1: {data}</div>;
}

export default Parent1;

// Parent2.js
import React from 'react';
import { useSelector } from 'react-redux';

function Parent2() {
  const data = useSelector(state => state.data);
  return <div>Data in Parent2: {data}</div>;
}

export default Parent2;

// Child.js
import React from 'react';
import { useDispatch } from 'react-redux';
import { fetchData } from './actions';

function Child() {
  const dispatch = useDispatch();

  return (
    <button onClick={() => dispatch(fetchData())}>
      Load Data
    </button>
  );
}

export default Child;
```

#### Redux Middleware:
  - `Middleware` in Redux is a way to **enhance the dispatch function**. 
  - Middleware can intercept every action sent to the store, then modify it, log it, delay it, ignore it, or perform other tasks before passing the action to the root reducer. 
  - This is crucial for handling side effects such as data fetching, as seen with redux-thunk.

#### Store Updates:

  - When an action is dispatched, the **Redux store's reducer calculates** the `new state` and ***replaces*** the `old state`. 
  - All listeners registered via subscribe are notified to re-render the React components based on the new state, maintaining a reactive data flow. 

<summary>
View Answer
</summary>
</details>


-----

7. Code example of communication between 2 parents which use the same child
8. What are semantic tags? write down sample HTML for a blog page with sidebar and list of blogs, tell some semantic tags you have worked on?
9.  difference between `<p>`, `<span>` and `<label>` tags when to use which tag.
10. what are block, inline elements what are the differences
11. `meta` tag to achieve responsiveness with syntax
12. Positions and movement of an element with each position (relative, absolute, fixed and sticky)
13. various display properties and what is the differences between them
14. media queries for specific screens
15. grid and flex-box
16. Recursion and use cases with example 
17. Hoisting
18. difference between declaring variables with let and var
19. call, apply and bind methods
20. webComponents (agnostic)
21. How to embed 2 or more component as a single component, and how to communicate between them
22. What is React Portal?
23. How do you efficiently work with Forms in react?