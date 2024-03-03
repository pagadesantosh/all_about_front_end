## 1.  What is Redux?
   
- Redux **is a predictable state container** for JavaScript applications. *(Yes, it can be used with any other JavaScript framework or library)*. 
- It ***helps you write applications that <ins>behave consistently</ins>, run in different environments*** (client, server, and native), and are easy to test.
-  With Redux, **<ins>the entire state of your application is kept in a store</ins>**, **and <ins>each component can access any state *without having to send down props* from one component to another</ins> that it needs from this store**.

- ##### There are `three` building parts: `actions`, `store`, and `reducers`.

#### Benefits and limitations of Redux:

**1. <ins>State transfer**</ins>

- State is stored together in a single place called the ‘store.’ 
- While you do not need to store all the state variables in the ‘store,’ it is especially important to when state is being shared by multiple components or in a more complex architecture. 
- It also allows you to call state data from any component easily.

**2. <ins>Predictability**</ins>

- Redux is **predictable state container for Javascript apps.**
- Because reducers are pure functions, the same result will always be produced when a same state and action are passed in.

**3. <ins>Maintainability**</ins>

- Redux provides a strict structure for how the code and state should be managed, which makes the architecture easy to replicate and scale for somebody who has previous experience with Redux.

**4. <ins>Ease of testing and debugging**</ins>

Redux makes it easy to test and debug your code since it offers powerful tools such as Redux DevTools in which you can time travel to debug, track your changes, and much more to streamline your development process.


-----

## 2. Explain pros and cons of Redux?

### Pros using redux:
- Central store (any component can access any state from the store)
- Store **<ins>persists the state of a component</ins> *even after the component has unmounted***.
- ***Prevents unnecessary re-renders***, as when the state changes <ins>**it returns new state which uses shallow copy.**</ins>
- Testing will be easy as UI and data management are separated.
- **History of state is maintained** which helps in implementing features like undo very easily.


### Cons using redux:
- No encapsulation. Any component can access the data which can cause security issues.
- Boilerplate code. Restricted design.
- ***As state is immutable in redux, the reducer updates the state by returning a new state every time*** which can cause excessive use of memory.

-----

## 3. Explain the concept of a `thunk` in Redux.
- Redux Thunk is a middleware that **lets you call action creators <ins>that return a function instead of an action object</ins>**. 
- The `primary` use of Redux Thunk is to ***handle asynchronous operations*** within the Redux ecosystem
- It **provides a way to delay the dispatch of an action, or to dispatch only if a certain condition is met**. 
- This capability is particularly useful for complex synchronous logic, such as conditional dispatching of actions, or for asynchronous processes like API calls.

<br/>

- <ins>**Asynchronous Actions**</ins>: In standard Redux, action creators return an action object, and these actions are immediately dispatched by the store.** Redux Thunk extends this model by allowing action creators to return a function**. This function can perform asynchronous operations (e.g., API requests) and dispatch actions based on the outcome of those operations.
<br/>

- <ins>**Conditional Dispatching**</ins>: Redux Thunk **allows for conditional dispatching of actions within its returned function**. This is useful when you want to dispatch actions only if certain conditions are met, avoiding unnecessary updates to the state or API calls.
<br/>

- <ins>**Complex Synchronous Logic**</ins>: Beyond asynchronous actions, **Thunks can be used to encapsulate complex synchronous logic that needs access to the dispatch method or the current state of the store**. <ins>This keeps the logic outside of components, making them cleaner and focusing them on the UI</ins> rather than on how the state is managed or updated.
<br/>

- <ins>**Access to `Dispatch` and `GetState`**</ins>: The functions returned by thunk action creators **receive the store's dispatch and getState methods as arguments**. This allows the action creators to dispatch other actions or access the current state of the Redux store as needed during asynchronous operations or complex logic.

-----

## 4. Example of a Redux Thunk Action Creator

```js
function fetchUserData(userId) {
  // This function is the thunk and gets dispatch and getState as arguments
  return async (dispatch, getState) => {
    dispatch({ type: 'USER_FETCH_REQUEST', userId });

    try {
      const response = await fetch(`https://api.example.com/user/${userId}`);
      const data = await response.json();
      dispatch({ type: 'USER_FETCH_SUCCESS', userId, data });
    } catch (error) {
      dispatch({ type: 'USER_FETCH_FAILURE', userId, error });
    }
  };
}

```

```js
npm install redux react-redux redux-thunk
```
```js
// Import the required libraries
import React from 'react';
import { createStore, applyMiddleware } from 'redux';
import { Provider } from 'react-redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers'; // Import your root reducer
import AppContent from './AppContent'; // This is your application's main component

// Create the Redux store, applying the thunk middleware
const store = createStore(
  rootReducer,
  applyMiddleware(thunk)
);

function App() {
  return (
    <Provider store={store}>
      <AppContent />
    </Provider>
  );
}

export default App;

```
------

## 5. What are redux core concepts?
   

![alt text](<images used/redux-components.jpg>)

### **1. <ins>Actions in Redux**</ins>
- Actions **are plain JavaScript objects** that represent the payloads of information that send data from your application to your store.
- They are the **only source of information for the store**
- Actions must have a `type` property that indicates the <ins>type of action being performed</ins>. `Types` should typically be **defined as string constants**. 
- Once an action is created, it is dispatched to the store to trigger updates to the state.

##### Key concepts related to actions in Redux:

1. <ins>**Action Creators**</ins>: 
   - These are **functions that create or return an action**. <ins>Instead of directly dispatching an action object, you often use action creators to encapsulate the process of creating an action</ins>.
<br/>
1. <ins>**Action Types**</ins>: 
   - These are usually **defined as string constants** and help identify the action that needs to be performed. Defining them as constants helps avoid typos and provides an easy way to manage all actions in larger applications.
<br/>

1. <ins>**Dispatching an Action**</ins>: 
   - This is the <ins>**process of sending an action to the Redux store to invoke state changes**</ins>. The store's dispatch function is used for this purpose.
<br/>

```js
const ADD_TODO = 'ADD_TODO';

// Action Creator
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  }
}

// Dispatching an Action (dispatch function is then used to send this action to the Redux store)
dispatch(addTodo('Learn Redux'));
```

### **2. <ins>Reducers**:</ins> 

- Reducers in Redux are **pure functions** that take the `current state` of an application and an `action` as arguments, and ***return a new state***. 
- The term "reducer" comes from the concept of a reducing function in functional programming, which is used to reduce a collection of values down to a single value

#### The key principles of reducers in Redux are:

1. <ins>**Pure Functions**:</ins> 
   - Reducers **must** be pure functions. 
   - This means they **should not produce side effects**, such as API calls or routing transitions, and they should not modify the state passed to them. 
   - Instead, **they should return a new object if any changes are made**.
<br/>

2. <ins>**State Shape**:</ins> 
   - The state shape (structure) is determined by the reducers. 
   - You can have multiple reducers, each managing its own part of the global state. 
   - The Redux <ins>**combineReducers helper function can be used to combine them into a single root reducer**</ins>.
<br/>

3. <ins>**Handling Actions**:</ins> 
   - Reducers **specify how the application's state changes in response to actions**. 
   - <ins>**They use the action's type**</ins> to determine how to transform the current state into a new state.
<br/>

4. <ins>**Immutability**:</ins> 
   - When changing the state, reducers must return a new object or array rather than modifying the existing state. 
   - This immutability principle ensures that Redux can efficiently track changes and update the UI.
<br/>

5. <ins>**Initialization and Resetting:**</ins>
   -  Reducers can set up the initial state and handle actions that reset the state back to the initial state.


```js
const initialState = {
  todos: []
};

function todoReducer(state = initialState, action) {
  switch (action.type) {
    case 'ADD_TODO':
      return {
        ...state,
        todos: [...state.todos, action.text]
      };
    case 'REMOVE_TODO':
      return {
        ...state,
        todos: state.todos.filter(todo => todo !== action.text)
      };
    default:
      return state;
  }
}
```

### **3. <ins>Store in Redux**</ins>

- A Store ***is an object that holds the whole state tree of your application***. 
- Whenever the `store` is updated, <ins>it will update the React components subscribed to it.</ins> 
- The store has the responsibility of `storing`, `reading`, and `updating state`.

```js
import React from 'react'
import { render } from 'react-dom'
import { Provider } from 'react-redux'
import { createStore } from 'redux'
import rootReducer from './reducers'
import App from './components/App'

const store = createStore(rootReducer)
 render (
   <Provider store="{store}">
     <App>
   </App></Provider>,
   document.getElementById('root')
 )
```

### **4. <ins>Dispatching Actions</ins>** 

- ##### This dispatch call sends an action to the store,

```js
store.dispatch({
  type: 'ADD_TODO',
  text: 'Learn Redux'
});

```

### **5. <ins>Subscribing to changes:</ins>**
- used to subscribe data/state from the Store.

```js
store.subscribe()
```

### **6. <ins>Middleware**</ins>

- Middlewares are **used to dispatch async functions**. 
- We configure Middleware's while creating a store.


```js
const store = createStore(reducers, initialState, middleware);
```

----


## 6.  What do you understand by "Single source of truth" in Redux?
  
- refers to the principle that the <ins>***state of your whole application is stored in an object tree within a single store***</ins>. 

- This means that instead of having multiple, possibly inconsistent sources of state scattered throughout your application, there is one central place where the state is managed and stored. 
  
1. <ins>**Predictability**</ins>: 
   - Because there is only one place where the state is stored, it becomes much easier to track changes, debug, and understand how state changes over time
   - This predictability is crucial for large applications, making them easier to maintain.
   <br/>

2. <ins>**Maintainability**</ins>:
   - With all state changes flowing through a centralized store, it's easier to impose rules on how state can be updated, ensuring consistency across the application. 
   - This centralized control aids in maintaining and scaling the application.
   <br/>

3. <ins>**Debugging**:</ins> 
   - The single state tree makes it possible to implement powerful debugging tools, such as logging every state change, traveling back and forth in time to understand how state mutations lead to bugs, and even rehydrating state from a previous session.
   <br/>

4. <ins>**Serialization**:</ins> 
   - Having the entire application state in one place **makes it possible to serialize the state (e.g., to localStorage) and deserialize it later**, potentially enabling features like undo/redo or saving the state of the application to be resumed later.
   <br/>

5. <ins>**Simplifies Data Flow**:</ins> 
   - The single source of truth simplifies data flow in the application by **adhering to unidirectional data flow**, <ins>*where state flows down from the store to the UI components*</ins>, and actions flow up from the components to update the state.

   <br/>

------

## 7. What are the features of Workflow in Redux?


- When using Redux with React, **states will no longer need to be lifted up**. Everything is handled by Redux. 
- Redux offers a solution for **storing all your application state in one place**, called a store.
- Components then **dispatch state changes to the store**, not directly to other components.
- The components **that need to be aware of state changes can subscribe to the store**.
- The store can be thought of as a "middleman" for all state changes in the application.
- With Redux involved, <ins>components don't communicate directly with each other</ins>. **Rather, all state changes must go through the single source of truth**, the store.

-----

## 8. Redux has three core principles:

1. <ins>**Single Source of Truth**:</ins> 
   -    The state of your whole application is stored in an object tree within a single store.

2. <ins>**State Is Read-Only**:</ins> 
   - The only way to change the state is to dispatch an action, an object describing what happened.
3. <ins>**Changes Are Made With Pure Functions**:</ins> 
   - To specify how the state tree is transformed by actions, you write pure reducers.


### The following are details of how Redux works:
- When UI Event triggers (OnClick, OnChange, etc) it can dispatch Actions based on the event.
- Reducers process Actions and return a new state as an Object.
- The new state of the whole application goes into a single Store.
- Components can easily subscribe to the Store.

-------

## 9.  What is difference between presentational component and container component in react redux?
    
- ***Represent a <ins>pattern for organizing code</ins>*** that helps in managing complexity, particularly in large applications. 
- This pattern helps in separating the concerns between how things look (UI) and how things work (logic and state management). 

##### Here's a breakdown of the differences:


###<ins>**Container Components**:</ins> 
   
- **Purpose**: 
  - Container components are **concerned with how things work**. They provide the `data` and `behavior` to presentational or other container components.
<br/>

- **State**: 
  - They are **more likely to maintain state and handle state updates**. They connect to the Redux store and dispatch actions to update the store based on user interactions.
<br/>

- **Redux**: 
  - They use Redux-specific functions like `connect` (in React-Redux bindings) to read from a Redux store and dispatch actions. With the introduction of hooks in React, container components might also use hooks like `useSelector` and `useDispatch` for a similar purpose.
<br/>

- **Reusability**: 
  - They are **less reusable since they are tightly coupled** with the business logic and data fetching mechanisms.

<ins>**Example**</ins>: A TodoListContainer component that fetches todo items from the Redux store and passes them to a TodoList presentational component to render.






### <ins>**Presentational Components**:</ins> 

- **Purpose**: 
  - Are primarily **concerned with how things look**. They render the UI based on the props passed to them.
<br/>

- **State**: 
  - They **usually don't manage state** (except for local UI state) and **receive data and callbacks exclusively via `props`**.
<br/>

- **Redux**: 
  - They are unaware of Redux. **They don't dispatch actions or directly interact with the Redux store**.
<br/>

- **Reusability**: 
  -  Since they focus on the UI without embedding business logic, they tend to be more reusable across different parts of the application or even in different applications..

<ins>**Example**</ins>: Button component that receives a label and an onClick callback as props.


- #### It's worth noting that with the advent of React Hooks (useState, useEffect, useContext, useReducer, and custom hooks), the distinction between presentational and container components <ins>*has become less clear and less necessary*</ins>.

----
## 10.  How to split the reducers?

- In Redux, splitting reducers is a common practice to manage the complexity of handling a large state object. 
- This process is known as `"reducer composition"` and is **facilitated by the combineReducers utility function provided by Redux**. 
- The <ins>***idea is to create multiple smaller reducer functions, each managing its own slice of the state, and then combine them into one root reducer</ins>***. Each of these smaller reducers is responsible for updating a specific piece of state based on the action dispatched.

#### Here's a step-by-step guide on how to split reducers:

### 1. <ins>Create Individual Reducers</ins>

```js
// todosReducer.js
function todosReducer(state = [], action) {
  switch (action.type) {
    case 'ADD_TODO':
      return [...state, action.payload];
    case 'REMOVE_TODO':
      return state.filter(todo => todo.id !== action.payload);
    // Add other cases as needed
    default:
      return state;
  }
}

// visibilityFilterReducer.js
function visibilityFilterReducer(state = 'SHOW_ALL', action) {
  switch (action.type) {
    case 'SET_VISIBILITY_FILTER':
      return action.payload;
    // Add other cases as needed
    default:
      return state;
  }
}
```
### 2. <ins>Combine Reducers</ins>



```js
import { combineReducers } from 'redux';
import todosReducer from './todosReducer';
import visibilityFilterReducer from './visibilityFilterReducer';

const rootReducer = combineReducers({
  todos: todosReducer,
  visibilityFilter: visibilityFilterReducer,
});

export default rootReducer;

```

### 3. <ins>Create the Redux Store</ins>

```js
import { createStore } from 'redux';
import rootReducer from './reducers'; // The combined reducers

const store = createStore(rootReducer);
```

----

## 11. How to create action creators with redux?

- Action creators in Redux **are functions that create (or return) action objects**.    
- `Actions` are plain JavaScript objects that describe "what happened" in your application
- These objects must have a type property indicating the type of action being performed, **and they can optionally have a payload property or any other fields** you deem necessary to describe the action.    
    
#### Step 1: Define Action Types    
  - First, define constants for your action types to avoid typos and simplify changes later on.

```js
// actionTypes.js
export const ADD_TODO = 'ADD_TODO';
export const REMOVE_TODO = 'REMOVE_TODO';

```
#### Step 2: Create Action Creators
- Create functions that return an action object. Each function corresponds to a specific action in your application.

```js
// actions.js
import { ADD_TODO, REMOVE_TODO } from './actionTypes';

// Action creator for adding a todo
export function addTodo(text) {
  return {
    type: ADD_TODO,
    payload: { text }
  };
}

// Action creator for removing a todo
export function removeTodo(id) {
  return {
    type: REMOVE_TODO,
    payload: { id }
  };
}
```

#### Step 3: Dispatch Actions in Components

- In your React components, use the useDispatch hook from react-redux to dispatch actions created by your action creators. This is assuming you're using functional components and the hooks API.


```js
import React, { useState } from 'react';
import { useDispatch } from 'react-redux';
import { addTodo } from './actions';

function TodoInput() {
  const [input, setInput] = useState('');
  const dispatch = useDispatch();

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!input.trim()) return;
    dispatch(addTodo(input));
    setInput('');
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={input}
        onChange={(e) => setInput(e.target.value)}
      />
      <button type="submit">Add Todo</button>
    </form>
  );
}
```

#### Step 4: Connect Redux State and Dispatch to Your Components
- For components that need to access the Redux state or dispatch actions, use the useSelector hook to access the state and the useDispatch hook to dispatch actions.

- If you're using class components, you would use the connect function instead to provide state and dispatch props to your components.


```js
import React from 'react';
import { useSelector } from 'react-redux';

function TodoList() {
  const todos = useSelector(state => state.todos);

  return (
    <ul>
      {todos.map(todo => (
        <li key={todo.id}>{todo.text}</li>
      ))}
    </ul>
  );
}
```



----
    
## 12.  How to set the dataflow using react with redux?
    
#### 1. Install Redux and React-Redux
```js
npm install redux react-redux
```

#### 2. Create Action Creators
```js
// actions/todoActions.js
export const addTodo = (todo) => {
  return {
    type: 'ADD_TODO',
    payload: todo,
  };
};

export const removeTodo = (todoId) => {
  return {
    type: 'REMOVE_TODO',
    payload: todoId,
  };
};
```

#### 3. Create Reducers
```js
// reducers/todosReducer.js
const initialState = {
  todos: [],
};

function todosReducer(state = initialState, action) {
  switch (action.type) {
    case 'ADD_TODO':
      return {...state, todos: [...state.todos, action.payload]};
    case 'REMOVE_TODO':
      return {...state, todos: state.todos.filter(todo => todo.id !== action.payload)};
    default:
      return state;
  }
}

export default todosReducer;
```

#### 4. Combine Reducers

```js
// reducers/index.js
import { combineReducers } from 'redux';
import todosReducer from './todosReducer';

const rootReducer = combineReducers({
  todos: todosReducer,
});

export default rootReducer;
```

#### 5. Create the Redux Store

```js
// store.js
import { createStore } from 'redux';
import rootReducer from './reducers';

const store = createStore(rootReducer);

export default store;
```

#### 6. Provide the Redux Store to React

```js
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import App from './App';
import store from './store';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

#### 7. Connect React Components to the Redux Store
- Use the connect function or the useSelector and useDispatch hooks in your components to access and modify the Redux store.


```js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { addTodo } from './actions/todoActions';

function TodoApp() {
  const todos = useSelector(state => state.todos.todos);
  const dispatch = useDispatch();

  const handleAddTodo = (todo) => {
    dispatch(addTodo(todo));
  };

  // Render your component UI here
}
```

```js
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { addTodo } from './actions/todoActions';

class TodoApp extends Component {
  handleAddTodo = (todo) => {
    this.props.addTodo(todo);
  };

  // Render your component UI here
}

const mapStateToProps = (state) => ({
  todos: state.todos.todos,
});

const mapDispatchToProps = {
  addTodo,
};

export default connect(mapStateToProps, mapDispatchToProps)(TodoApp);
```

----------------

    
## 13. How can I represent "side effects" such as AJAX calls? Why do we need things like "action creators", "thunks", and "middleware" to do async behavior?    
    
- Side effects means that **code is no longer purely a function of its inputs, and the interactions with the outside world** are known as "side effects".
- Redux is inspired by functional programming, and out of the box, **has no place for side effects to be executed**. In particular, `reducer` functions **must always be pure functions** of (state, action) => newState.
- However, <ins>**Redux's middleware (eg. Redux Thunk, Redux Saga) makes it possible to intercept dispatched actions and add additional complex behavior** around them, including side effects.</ins>
  
----------------

## 14. What is the '@' (at symbol) in the Redux @connect decorator?

- `Decorators` make it possible to ***annotate and modify classes and properties <ins>at design time***</ins>.


#### Without a decorator

```js
import React from 'react'
import * as actionCreators from './actionCreators'
import { bindActionCreators } from 'redux'
import { connect } from 'react-redux'

function mapStateToProps(state) {
  return { todos: state.todos }
}

function mapDispatchToProps(dispatch) {
  return { actions: bindActionCreators(actionCreators, dispatch) }
}

class MyApp extends React.Component {
  // ...define your main app here
}

export default connect(mapStateToProps, mapDispatchToProps)(MyApp)
```


#### With decorator
```js
import React from 'react'
import * as actionCreators from './actionCreators'
import { bindActionCreators } from 'redux'
import { connect } from 'react-redux'

// mapStateToProps is a function that maps the state from the Redux store to the props of the component. 
function mapStateToProps(state) {
  return { todos: state.todos }
}

// mapDispatchToProps does a similar thing but for dispatching actions.
function mapDispatchToProps(dispatch) {
  return { actions: bindActionCreators(actionCreators, dispatch) }
}

@connect(mapStateToProps, mapDispatchToProps)
export default class MyApp extends React.Component {
  // ...define your main app here
}
```


----

## 15. What is the difference between React State vs Redux State?

- `React state` is **stored locally within a component**. When it needs to be shared with other components, it is passed down through props. 


- When using `Redux`, **state is stored globally in the Redux store**. Any component that needs access to a value may subscribe to the store and gain access to that value.




------

## 16. What is the best way to access redux store outside a react component?

- Accessing the Redux store outside a React component is **commonly needed for dispatching actions** or **accessing the state in non-component files**, such as in middleware, services, or helpers

#### Step 1: Create and Export the Store 

```js
import { createStore, applyMiddleware } from 'redux';
import rootReducer from './reducers';
import thunk from 'redux-thunk';

const store = createStore(
  rootReducer,
  applyMiddleware(thunk)
);

export default store;
```

#### Step 2: Import and Use the Store
```js
import store from './path/to/your/store';

// Dispatching an action
store.dispatch({ type: 'ACTION_TYPE' });

// Accessing the state
const currentState = store.getState();
```

<ins>**Good To Know:**</ins>
- **Singleton Pattern**: 
  - By `exporting` and `importing` the `store`, **you're essentially using it as a singleton**. 
  - This ensures that the same store instance is used <ins>***throughout your application, maintaining consistency in your application's state management***</ins>.

----

## 17. How to add multiple middleware to redux?
- In Redux, <ins>**middleware allows you to write logic that can be inserted into the dispatch process of actions**</ins> before they reach the reducer. 
- This is useful for `logging actions`, `performing asynchronous tasks`, and more
- To add multiple middleware to Redux, <ins>**you use the applyMiddleware function from Redux in combination with the createStore function**</ins>.
  

#### Step 1: Import the Middleware and Redux Methods: 

```js
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import logger from 'redux-logger';
```

#### Step 2: Combine Middleware: 
- Use `applyMiddleware()` to combine your middleware.
- You can pass all the middleware you want to use as arguments to this function.
- **If you have more than one middleware, <ins>just separate them with commas**</ins>

```js
const middleware = applyMiddleware(thunk, logger);
```

#### Step 3: Apply Middleware to the Store: 
- When creating the Redux store with `createStore`, **you can now apply the combined middleware**. 
- The `createStore` function takes up to three arguments: the `rootReducer`, the `initialState`, and the `enhancer` (in this case, the middleware).

```js
const store = createStore(
  rootReducer,
  initialState,
  middleware
);
```

#### Step 4: If you are using Redux DevTools Extension: 
- You might want to **compose the middleware with the dev tools extension**. 
- In that case, you would use the `compose` function from Redux like so:

```js
import { createStore, applyMiddleware, compose } from 'redux';

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
const store = createStore(
  rootReducer,
  initialState,
  composeEnhancers(
    applyMiddleware(thunk, logger)
  )
);
```    
----------

## 18. What are the differences between redux-saga and redux-thunk?


- `redux-saga` and `redux-thunk` are both middleware libraries for Redux, a state management library for JavaScript applications, most commonly used with React. 
-  They are used to handle side effects in your Redux application, such as asynchronous actions like fetching data from an API or complex synchronous operations.







#### **1. Redux Thunk**
- Redux Thunk is a middleware that lets you call action creators that <ins>**return a function instead of an action object**</ins>.
- **That function receives the store's dispatch method**, <ins>which is then used to dispatch regular synchronous actions inside the body of the function once the asynchronous operations have completed.</ins>


![alt text](<images used/redux-thunk-image.jpeg>)

```js
npm i --save react-redux redux redux-logger redux-saga redux-thunk
```

- `Thunk` **is a function** <ins>***which optionally takes some parameters and returns another function***</ins>, it takes `dispatch` and `getState` functions and both of these are supplied by Redux Thunk middleware.


```js
// Action Creators with redux-thunk
function fetchData() {
  return (dispatch) => {
    dispatch({ type: 'FETCH_DATA_BEGIN' });
    return fetch('https://api.example.com/data')
      .then(response => response.json())
      .then(json => dispatch({ type: 'FETCH_DATA_SUCCESS', payload: json }))
      .catch(error => dispatch({ type: 'FETCH_DATA_FAILURE', error }));
  };
}

// Using the thunk in a component
import React, { useEffect } from 'react';
import { useDispatch } from 'react-redux';

const MyComponent = () => {
  const dispatch = useDispatch();
  
  useEffect(() => {
    dispatch(fetchData());
  }, [dispatch]);
  
  return <div>Content</div>;
};
```

#### **2. redux saga**
- uses ES6 generators to make asynchronous flow easy to read, write, and test. Sagas are implemented as generator functions that yield objects to the redux-saga middleware
- In saga, we can test our asynchronous flows easily and our actions stay pure. It organized complicated asynchronous actions easily and make then very readable and the saga has many useful tools to deal with asynchronous actions.


![alt text](<images used/redux flow.png>)

```js
// Sagas
import { call, put, takeEvery } from 'redux-saga/effects';

function* fetchData(action) {
  try {
    const data = yield call(() => fetch('https://api.example.com/data').then(res => res.json()));
    yield put({type: 'FETCH_DATA_SUCCESS', payload: data});
  } catch (e) {
    yield put({type: 'FETCH_DATA_FAILURE', message: e.message});
  }
}

/*
  Starts fetchData on each dispatched `FETCH_DATA_BEGIN` action.
  Allows concurrent fetches of data.
*/
function* mySaga() {
  yield takeEvery('FETCH_DATA_BEGIN', fetchData);
}

export default mySaga;

// Setting up the Saga middleware
import { createStore, applyMiddleware } from 'redux';
import createSagaMiddleware from 'redux-saga';
import rootReducer from './reducers';
import mySaga from './sagas';

const sagaMiddleware = createSagaMiddleware();
const store = createStore(
  rootReducer,
  applyMiddleware(sagaMiddleware)
);

sagaMiddleware.run(mySaga);
```


#### Key Differences in Usage:
**Thunk Approach**: 
- In `redux-thunk`, the asynchronous logic is placed inside the action creator itself. 
- The **action creator returns a function that performs the async operation and then dispatches actions based on the outcome**.

**Saga Approach:** 
- In `redux-saga`, the asynchronous logic is separated from action creators. 
- Sagas listen for actions dispatched to the store and then perform side effects. 
- Sagas use yield to make asynchronous calls easy to read and write in a synchronous-like fashion.
-------

19. Explain Redux form with an example?

- Redux Form is a **library for managing form state in Redux**. 
- It provides a way to handle form inputs and submissions using Redux, with form validation and submission capabilities. 
- Redux Form <ins>***works by storing form state in the Redux store, allowing you to easily connect your forms to Redux***</ins>
- It utilizes `higher-order components` and `decorators` **to connect your forms to the Redux store**.


#### Step 1: Setup Redux Form

```js
import { createStore, combineReducers } from 'redux';
import { reducer as formReducer } from 'redux-form';

const rootReducer = combineReducers({
  // ...your other reducers here
  form: formReducer // <--- Mounted at 'form'
});

const store = createStore(rootReducer);
```
#### Step 2: Create a Form Component

- Use `reduxForm()` to connect your form component to Redux Form. 
- Define your form fields using the Field component and specify the validation logic.

```js
import React from 'react';
import { Field, reduxForm } from 'redux-form';

// Validation function
const validate = values => {
  const errors = {};
  if (!values.username) {
    errors.username = 'Required';
  } else if (values.username.length > 15) {
    errors.username = 'Must be 15 characters or less';
  }
  if (!values.email) {
    errors.email = 'Required';
  } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(values.email)) {
    errors.email = 'Invalid email address';
  }
  return errors;
};

// Custom input component
const renderField = ({ input, label, type, meta: { touched, error } }) => (
  <div>
    <label>{label}</label>
    <div>
      <input {...input} type={type} />
      {touched && error && <span>{error}</span>}
    </div>
  </div>
);

// Form component
let SimpleForm = props => {
  const { handleSubmit, pristine, reset, submitting } = props;
  return (
    <form onSubmit={handleSubmit}>
      <Field name="username" type="text" component={renderField} label="Username" />
      <Field name="email" type="email" component={renderField} label="Email" />
      <div>
        <button type="submit" disabled={submitting}>Submit</button>
        <button type="button" disabled={pristine || submitting} onClick={reset}>
          Clear Values
        </button>
      </div>
    </form>
  );
};

// Connecting the form component to Redux Form
SimpleForm = reduxForm({
  form: 'simple', // a unique identifier for this form
  validate, // validation function
})(SimpleForm);

export default SimpleForm;
```

#### Step 3: Use the Form in Your Application

```js
import React from 'react';
import SimpleForm from './SimpleForm'; // Import your form component

const App = () => (
  <div>
    <h2>Simple Form Example</h2>
    <SimpleForm />
  </div>
);

export default App;
```

**Explanation**:
- **Redux Form Reducer**: The form reducer is mounted on the form key of your root reducer to manage form states.
- **Form Component**: You create a form component and decorate it with reduxForm(), passing configuration options such as the form's name and validation function.
- **Field Component:** Use the Field component to define inputs in your form, specifying the name of the field, the type of input, and the component to render the field.
- **Validation**: Validation logic is defined in a function that receives the form's values, checks for errors, and returns an object with any errors found.

--- 

20. How to reset state in redux?
    
21. What are the differences between call and put in redux-saga?
22. What is the mental model of `redux-saga`?
23. How `Relay` is different from Redux?
24. When would `bindActionCreators` be used in react/redux?
25. What is `mapStateToProps` and `mapDispatchToProps`?
26. What is `reselect` and how it works?
27. What are the different ways to dispatch actions in Redux?
28. How to use Redux for Error Handling?
29. Explain the purpose of `Redux middleware`.

30. How does Redux handle `asynchronous actions`?

31. Discuss the use of the `compose` function in Redux.

32. How would you `test` Redux-connected components?

33. Discuss the concept of `middleware chaining` in Redux.

34. What is the purpose of the `Redux DevTools` extension?



35. Discuss the significance of the `payload` in a Redux action.

36. Explain the need for the `connect` function in React-Redux.

37. Discuss the principles of `normalizing state` shape in Redux.



38. Discuss the use of `memoization` in React-Redux applications.

39. Describe the role of the `Provider` component in React-Redux.

40. How does the Redux store `subscribe` to changes in the state?

41. Discuss the role of `selectors` in optimizing Redux state access.

42. Explain the purpose of the `applyMiddleware` function in Redux.

43. How can you handle `optimistic updates` in a Redux application?



44. Explain the concept of `immutability` and its importance in Redux.

45. `Compare` Redux and Context API in React for state management.
    
46. How would you `integrate` Redux with React Router for navigation?

47. How can you `handle forms` in a Redux-powered React application?

48. Explain the concept of `time-travel debugging`with Redux DevTools.

49. Discuss the concept of `middleware` in Redux and provide examples.

50. Explain the purpose of the `redux-persist library` in a Redux application.

51. How can you handle `authentication` and `authorization` in a Redux app?

52. How would you `optimize` the performance of a React-Redux application?
   

53. How can you `avoid` `unnecessary re-rendering` in a React-Redux application?

54. Explain the purpose of the `createSelector` function from the Reselect library.

55. Discuss the `benefits` and `drawbacks` of using Redux in a small-scale application.

56. Discuss the `advantages` and `disadvantages` of using Redux in a large-scale application.