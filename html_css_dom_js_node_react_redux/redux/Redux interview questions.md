1. #### What is Redux?

- Redux **is a predictable state container** for JavaScript applications. *(Yes, it can be used with any other JavaScript framework or library)*. 
- It ***helps you write applications that <ins>behave consistently</ins>, run in different environments*** (client, server, and native), and are easy to test.
-  With Redux, **<ins>the entire state of your application is kept in a store</ins>**, **and <ins>each component can access any state *without having to send down props* from one component to another</ins> that it needs from this store**.

- ##### There are three building parts: `actions`, `store`, and `reducers`.

**Benefits and limitations of Redux**

**1. State transfer**

- State is stored together in a single place called the ‘store.’ 
- While you do not need to store all the state variables in the ‘store,’ it is especially important to when state is being shared by multiple components or in a more complex architecture. 
- It also allows you to call state data from any component easily.

**2. Predictability**

- Redux is **predictable state container for Javascript apps.**
- Because reducers are pure functions, the same result will always be produced when a same state and action are passed in.

**3. Maintainability**

- Redux provides a strict structure for how the code and state should be managed, which makes the architecture easy to replicate and scale for somebody who has previous experience with Redux.

**4. Ease of testing and debugging**

Redux makes it easy to test and debug your code since it offers powerful tools such as Redux DevTools in which you can time travel to debug, track your changes, and much more to streamline your development process.

-------

2. #### Explain pros and cons of Redux?

**Pros using redux**:
- Central store (any component can access any state from the store)
- Store **<ins>persists the state of a component</ins> *even after the component has unmounted***.
- ***Prevents unnecessary re-renders***, as when the state changes <ins>**it returns new state which uses shallow copy.**</ins>
- Testing will be easy as UI and data management are separated.
- **History of state is maintained** which helps in implementing features like undo very easily.


**Cons using redux:**
- No encapsulation. Any component can access the data which can cause security issues.
- Boilerplate code. Restricted design.
- ***As state is immutable in redux, the reducer updates the state by returning a new state every time*** which can cause excessive use of memory.

-----

3. Explain the concept of a `thunk` in Redux.
- Redux Thunk is a middleware that **lets you call action creators <ins>that return a function instead of an action object</ins>**. 
- The `primary` use of Redux Thunk is to ***handle asynchronous operations*** within the Redux ecosystem
- It **provides a way to delay the dispatch of an action, or to dispatch only if a certain condition is met**. 
- This capability is particularly useful for complex synchronous logic, such as conditional dispatching of actions, or for asynchronous processes like API calls.


**Asynchronous Actions**: In standard Redux, action creators return an action object, and these actions are immediately dispatched by the store.** Redux Thunk extends this model by allowing action creators to return a function**. This function can perform asynchronous operations (e.g., API requests) and dispatch actions based on the outcome of those operations.

**Conditional Dispatching**: Redux Thunk **allows for conditional dispatching of actions within its returned function**. This is useful when you want to dispatch actions only if certain conditions are met, avoiding unnecessary updates to the state or API calls.

**Complex Synchronous Logic**: Beyond asynchronous actions, **Thunks can be used to encapsulate complex synchronous logic that needs access to the dispatch method or the current state of the store**. <ins>This keeps the logic outside of components, making them cleaner and focusing them on the UI</ins> rather than on how the state is managed or updated.

**Access to `Dispatch` and `GetState`**: The functions returned by thunk action creators **receive the store's dispatch and getState methods as arguments**. This allows the action creators to dispatch other actions or access the current state of the Redux store as needed during asynchronous operations or complex logic.

#### Example of a Redux Thunk Action Creator

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



------------
4. Explain the purpose of `Redux middleware`.

5. How does Redux handle `asynchronous actions`?

6. Discuss the use of the `compose` function in Redux.

7. How would you `test` Redux-connected components?

8. Discuss the role of the `initialState` in a Redux reducer.

9. Discuss the concept of `middleware chaining` in Redux.

10. What is the purpose of the `Redux DevTools` extension?

11. How do you handle `side effects` in Redux applications?

12. Discuss the significance of the `payload` in a Redux action.

13. Explain the need for the `connect` function in React-Redux.

14. Discuss the principles of `normalizing state` shape in Redux.

15. Describe the role of the `Redux store` in a React application.

16. Explain the significance of the `action type` in a Redux action.

17. Discuss the use of `memoization` in React-Redux applications.

18. Describe the role of the `Provider` component in React-Redux.

19. How does the Redux store `subscribe` to changes in the state?

20. Discuss the role of `selectors` in optimizing Redux state access.

21. Explain the purpose of the `applyMiddleware` function in Redux.

22. How can you handle `optimistic updates` in a Redux application?

23. What is the purpose of the `combineReducers` function in Redux?

24. Explain the concept of `immutability` and its importance in Redux.

25. `Compare` Redux and Context API in React for state management.
    
26. How would you `integrate` Redux with React Router for navigation?

27. How can you `handle forms` in a Redux-powered React application?

28. Explain the concept of `time-travel debugging`with Redux DevTools.

29. Discuss the concept of `middleware` in Redux and provide examples.

30. Discuss the difference between `actions` and `action creators` in Redux.

31. Explain the purpose of the `redux-persist library` in a Redux application.

32. How can you handle `authentication` and `authorization` in a Redux app?

33. How would you `optimize` the performance of a React-Redux application?

34. Explain the `difference` between the terms `"action"` and `"reducer"` in Redux.
    

35. How can you `avoid` `unnecessary re-rendering` in a React-Redux application?

36. Explain the purpose of the `createSelector` function from the Reselect library.

37. Discuss the `benefits` and `drawbacks` of using Redux in a small-scale application.

38. Discuss the `advantages` and `disadvantages` of using Redux in a large-scale application.


39. #### What are redux core concepts?

![alt text](<images used/redux-components.jpg>)

#### **1. Actions in Redux**
- Actions **are plain JavaScript objects** that represent the payloads of information that send data from your application to your store.
- They are the **only source of information for the store**
- Actions must have a `type` property that indicates the <ins>type of action being performed</ins>. `Types` should typically be **defined as string constants**. 
- Once an action is created, it is dispatched to the store to trigger updates to the state.

#### Key concepts related to actions in Redux:

1. **Action Creators**: These are **functions that create or return an action**. <ins>Instead of directly dispatching an action object, you often use action creators to encapsulate the process of creating an action</ins>.
<br/>
2. **Action Types**: These are usually **defined as string constants** and help identify the action that needs to be performed. Defining them as constants helps avoid typos and provides an easy way to manage all actions in larger applications.
<br/>

3. **Dispatching an Action**: This is the <ins>**process of sending an action to the Redux store to invoke state changes**</ins>. The store's dispatch function is used for this purpose.
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

#### **2. Reducers**: 

- Reducers in Redux are **pure functions** that take the `current state` of an application and an `action` as arguments, and ***return a new state***. 
- The term "reducer" comes from the concept of a reducing function in functional programming, which is used to reduce a collection of values down to a single value

The key principles of reducers in Redux are:

1. **Pure Functions**: 
   - Reducers **must** be pure functions. 
   - This means they **should not produce side effects**, such as API calls or routing transitions, and they should not modify the state passed to them. 
   - Instead, **they should return a new object if any changes are made**.
<br/>

2. **State Shape**: 
   - The state shape (structure) is determined by the reducers. 
   - You can have multiple reducers, each managing its own part of the global state. 
   - The Redux <ins>**combineReducers helper function can be used to combine them into a single root reducer**</ins>.
<br/>

3. **Handling Actions**: 
   - Reducers **specify how the application's state changes in response to actions**. 
   - <ins>**They use the action's type**</ins> to determine how to transform the current state into a new state.
<br/>

4. **Immutability**: 
   - When changing the state, reducers must return a new object or array rather than modifying the existing state. 
   - This immutability principle ensures that Redux can efficiently track changes and update the UI.
<br/>

5. **Initialization and Resetting:**
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

#### **3. Store in Redux**

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

#### Dispatching Actions 

- ##### This dispatch call sends an action to the store,

```js
store.dispatch({
  type: 'ADD_TODO',
  text: 'Learn Redux'
});

```

#### Subscribing to changes 
- used to subscribe data/state from the Store.

```js
store.subscribe()
```

#### Middleware

- Middlewares are **used to dispatch async functions**. 
- We configure Middleware's while creating a store.


```js
const store = createStore(reducers, initialState, middleware);
```



----

40.   What do you understand by "Single source of truth" in Redux?

- refers to the principle that the <ins>***state of your whole application is stored in an object tree within a single store***</ins>. 

- This means that instead of having multiple, possibly inconsistent sources of state scattered throughout your application, there is one central place where the state is managed and stored. 
  
1. **Predictability**: 
   - Because there is only one place where the state is stored, it becomes much easier to track changes, debug, and understand how state changes over time
   - This predictability is crucial for large applications, making them easier to maintain.
   <br/>

2. **Maintainability**:
   - With all state changes flowing through a centralized store, it's easier to impose rules on how state can be updated, ensuring consistency across the application. 
   - This centralized control aids in maintaining and scaling the application.
   <br/>

3. **Debugging**: 
   - The single state tree makes it possible to implement powerful debugging tools, such as logging every state change, traveling back and forth in time to understand how state mutations lead to bugs, and even rehydrating state from a previous session.
   <br/>

4. **Serialization**: 
   - Having the entire application state in one place **makes it possible to serialize the state (e.g., to localStorage) and deserialize it later**, potentially enabling features like undo/redo or saving the state of the application to be resumed later.
   <br/>

5. **Simplifies Data Flow**: 
   - The single source of truth simplifies data flow in the application by **adhering to unidirectional data flow**, <ins>*where state flows down from the store to the UI components*</ins>, and actions flow up from the components to update the state.

   <br/>

-----

41.  What are the features of Workflow in Redux?


- When using Redux with React, **states will no longer need to be lifted up**. Everything is handled by Redux. 
- Redux offers a solution for **storing all your application state in one place**, called a store.
- Components then **dispatch state changes to the store**, not directly to other components.
- The components **that need to be aware of state changes can subscribe to the store**.
- The store can be thought of as a "middleman" for all state changes in the application.
- With Redux involved, <ins>components don't communicate directly with each other</ins>. **Rather, all state changes must go through the single source of truth**, the store.


### Redux has three core principles:

1. **Single Source of Truth**: 
   -    The state of your whole application is stored in an object tree within a single store.

2. **State Is Read-Only**: 
   - The only way to change the state is to dispatch an action, an object describing what happened.
3. **Changes Are Made With Pure Functions**: 
   - To specify how the state tree is transformed by actions, you write pure reducers.


The following are details of how Redux works:
- When UI Event triggers (OnClick, OnChange, etc) it can dispatch Actions based on the event.
- Reducers process Actions and return a new state as an Object.
- The new state of the whole application goes into a single Store.
- Components can easily subscribe to the Store.

-----

4.  What is difference between presentational component and container component in react redux?
5.  Explain the role of Reducer?
6.  How to split the reducers?
7.  How to create action creators react with redux?
8.  How to set the dataflow using react with redux?
9.  What are the three principles that Redux follows?
10. How can I represent "side effects" such as AJAX calls? Why do we need things like "action creators", "thunks", and "middleware" to do async behavior?    
11. What is the '@' (at symbol) in the Redux @connect decorator?
12. What is the difference between React State vs Redux State?
13. What is the best way to access redux store outside a react component?
14. How to add multiple middleware to redux?
15. How to set initial state in Redux? 
16. What is the purpose of the constants in Redux?
17. What are the differences between redux-saga and redux-thunk?
18. Explain Redux form with an example?
19. How to reset state in redux?
20. Why are Redux state functions called as reducers?
21. What are the differences between call and put in redux-saga?
22. What is the mental model of `redux-saga`?
23. How `Relay` is different from Redux?
24. When would `bindActionCreators` be used in react/redux?
25. What is `mapStateToProps` and `mapDispatchToProps`?
26. What is `reselect` and how it works?
27. What are the different ways to dispatch actions in Redux?
28. How to use Redux for Error Handling?
