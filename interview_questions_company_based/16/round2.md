### 1. What are the hooks ?
- React hooks **are functions** that let you "hook into" React state and lifecycle features from function components. 
- They were **introduced in React 16.8** <ins>**to enable state management and side-effects**</ins> in functional components, 

1. `useState`: 
   - This hook **lets you add state** to functional components. You can initialize it with a value and it returns a pair: the current state and a function that updates it.
  <br/>

2. `useEffect`: 
   - This hook **lets you perform side effects** in functional components. 
   - It's **similar** to lifecycle methods `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` **in class components**. 
   - <ins>You can use it to fetch data, set up a subscription, or manually change the DOM in React components.</ins>
  <br/>

3. `useContext`: 
   - This hook **<ins>lets you subscribe to React context</ins> without introducing nesting**. 
  <br/>

4. `useReducer`:
   -  An **alternative to `useState`**. 
   -  It's usually **preferable for managing state logic that <ins>involves multiple sub-values</ins>** or when the next state depends on the previous one.
  <br/>
  
5. `useCallback`: 
   - This hook **returns a memoized callback function**. 
   - This is <ins>**useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders**</ins>.
  <br/>

6. `useMemo`: 
   - <ins>**Returns a memoized value**</ins>. 
   - This hook is <ins>**used to optimize performance by memorizing expensive functions**</ins> so that they are not re-run on every render unless their dependencies change.
  <br/>

7. `useRef`:
   - This hook **returns a mutable ref object** whose current property is initialized to the passed argument. 
   - It can be **used to store a mutable value <ins>that does not cause re-rendering when updated**</ins>.
  <br/>

8. `useImperativeHandle`: 
   - This hook is <ins>**used with forwardRef to customize the instance value**</ins> that is exposed to parent components when using refs.
  <br/>

9. `useLayoutEffect`: 
   - **Similar to useEffect, but it fires synchronously after all DOM mutations**. 
   - Use this <ins>**to read layout from the DOM and re-render synchronously**</ins>.
  <br/>

10. `useDebugValue`: 
    - Can be used to display a label for custom hooks in React DevTools.
---

### 2. How to improve the performance of an application ?

#### 1. HTML:
 - **Minimize DOM depth**: 
   - A **deeply nested DOM can slow down page performance** as it increases the time browsers spend to render content.
  - **Clean and semantic markup**: 
    - Use semantic HTML5 elements (`<main>`, `<article>`, `<section>`, etc.) which aid in the accessibility and can potentially optimize browser rendering processes.

#### 2. CSS
- **Optimize CSS delivery**: 
  - <ins>Use critical CSS techniques to **include only the styles necessary for the initial render** in the head of your HTML, **and defer non-critical CSS.**</ins>

- **Efficient selectors**: 
  - Complex selectors can slow down page rendering <ins>**as they require more processing</ins> to determine which elements they apply to**. 
  - Keep selectors simple and avoid overly specific ones.
- **Reduce reflows and repaints**: 
  - Minimize changes to the layout (reflows) and visual modifications (repaints) of pages, as these operations are costly. 
  - Use `transform` and `opacity` changes for animations when possible, as they can be optimized by the browser.

#### 3. JavaScript
- **Minimize and defer JavaScript loading**: 
  - Minimize the amount of JavaScript needed to render the page and defer loading scripts that are not necessary for the initial page render.
- **Use Web Workers for heavy computation**: 
  - <ins>**Offload heavy computations**</ins> to Web Workers to keep the UI thread free for rendering and interaction.
- **Optimize and debounce event listeners**: 
  - Especially for `scroll` or `resize` events, debounce your functions to limit the number of times they are called.
  
#### 4. React
- **Use PureComponent and React.memo**: 
  - These components and higher-order components **help prevent unnecessary re-renders** by doing shallow prop and state comparison.
- **Code splitting**: 
  - Use dynamic import() syntax or libraries like `React.lazy` and `Suspense` **to split your code into smaller chunks** and load them only when needed.
- **Optimize state updates**: 
  - Ensure that **state updates are batched when possible** and avoid unnecessary state changes.
- **Use the Profiler API**: 
  - This API helps in measuring the "cost" of rendering and **helps <ins>identify parts of the app that are slow**</ins>.

#### 5. Web Browsers
- **Caching**: 
  - Leverage **browser caching to store frequently accessed resources on the client-side**, reducing loading times on subsequent visits.
- **Preloading and prefetching resources**: 
  - Use `<link rel="preload">` for critical resources and `<link rel="prefetch">` for resources that <ins>**might be needed in the future**.</ins>
- **Optimize images**: 
  - Use modern, efficient image formats like `WebP`, `AVIF`, and ensure images are responsive by serving scaled images based on the device.

#### 6. General Best Practices
- **Performance Monitoring Tools**: 
  - Utilize tools like `Google Lighthouse`, `WebPageTest`, and `Chrome DevTools` to analyze and monitor performance.
- **HTTP/2**: 
  - Where possible, use `HTTP/2` as it supports multiplexing and server push, which can improve the loading times of web pages.
- **SSL/TLS Optimization**: 
  - Use SSL/TLS efficiently as the handshake can be costly. 
  - <ins>**Session resumption can help reduce the time needed to establish secure connections**</ins>.

----

### 3. Write HTML to display cards side by side ?

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Side by Side Cards</title>
<style>
  .card-container {
    display: flex;          
    justify-content: space-around;
    align-items: stretch;   
    padding: 20px;          
  }
  .card {
    width: 30%;            
    padding: 20px;         
    box-shadow: 0 4px 8px rgba(0,0,0,0.1); 
    background: white;     
    margin: 10px;          
  }
</style>
</head>
<body>

<div class="card-container">
  <div class="card">
    <h3>Card 1</h3>
    <p>This is the first card. It contains some example text to demonstrate the card layout.</p>
  </div>
  <div class="card">
    <h3>Card 2</h3>
    <p>This is the second card. It continues to provide content similar to what might be seen in a standard card layout.</p>
  </div>
  <div class="card">
    <h3>Card 3</h3>
    <p>This is the third card. Each card has the same width and padding, aligning neatly in a row.</p>
  </div>
</div>
</body>
</html>

```

  ![alt text](/interview_questions_company_based/16/imagesUsed/displayCards.png)

------

### 4. useMemo vs. useCallback ?

-  both `useMemo` and `useCallback` are hooks that **help you <ins>optimize the performance of your components**</ins> by memorizing expensive calculations or functions. 

#### `useMemo`:
- is used to <ins>**memorize the results of an expensive calculation**</ins>. 
- If the <ins>*dependencies of this calculation have not changed*, **React will skip executing it again** and reuse the last returned value</ins>. 
- This can be helpful in avoiding costly recalculations each time the component re-renders, which is particularly useful if the calculation is dependent on props or state that doesn't change frequently.

```js
import React, { useMemo, useState } from 'react';

function SortedList({ items }) {
  // Use useMemo to only re-sort the items when the 'items' array changes
  // to ensure that the sorting computation is not unnecessarily repeated on every render.
  const sortedItems = useMemo(() => {
    console.log("Sorting items");
    return [...items].sort();
  }, [items]);

  return (
    <ul>
      {sortedItems.map(item => (
        <li key={item}>{item}</li>
      ))}
    </ul>
  );
}

// Usage in another component
function App() {
  const [items, setItems] = useState(['orange', 'apple', 'banana']);

  // Function to shuffle the items array
  // calculates a sorted list based on an input list that only changes when a user performs a specific action
  const shuffleItems = () => {
    setItems(items => {
      const result = [...items];
      result.sort(() => Math.random() - 0.5);
      return result;
    });
  };

  return (
    <div>
      <button onClick={shuffleItems}>Shuffle Items</button>
      <SortedList items={items} />
    </div>
  );
}

export default App;
```

- Use `useMemo` <ins>**when you need to memorize the result of a computation or derive new data from props or state.**</ins>

----

#### `useCallback`:

- The `useCallback` hook is used <ins>**to memorize a function instance**</ins>. 
- This is <ins>**useful when passing callback functions to optimized child components that rely on reference equality to avoid unnecessary renders**</ins>. 
- If the function’s dependencies don’t change, **React reuses the same function instance** between renders.

```js
import React, { useCallback, useState } from 'react';

function ExpensiveButton({ onCalculate }) {
  console.log("Button rendered");
  return <button onClick={onCalculate}>Calculate</button>;
}

function App() {
  const [count, setCount] = useState(0);

  // Use useCallback to prevent unnecessary re-renders of ExpensiveButton
  const handleCalculate = useCallback(() => {
    console.log("Calculation performed");
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <ExpensiveButton onCalculate={handleCalculate} />
    </div>
  );
}

export default App;
```

- Use `useCallback` <ins>**when you need to memorize a callback function to pass it as a prop to child components**</ins>, especially when these children are optimized to avoid unnecessary re-renders.

-----

### 5. About React.lazy?

- `React.lazy` **is a function** in React that <ins>**allows you to load components lazily through code splitting**</ins>. 
- This means that the component will only be loaded when it is needed, rather than loading it up front with the rest of the bundle.
- This can significantly improve the performance of your application <ins>**by reducing the initial load time**</ins>.
- `React.lazy` **works with dynamic imports**, a feature that <ins>**allows you to import modules asynchronously**</ins>. 
- Used in conjunction with the `Suspense` component which allows you to specify a loading indicator while the lazy component is being loaded.

```js
import React, { Suspense } from 'react';

// Lazily import the ChartComponent
const LazyChartComponent = React.lazy(() => import('./ChartComponent'));

function App() {
  return (
    <div>
      <h1>Welcome to My App</h1>
      <Suspense fallback={<div>Loading Chart...</div>}>
        <LazyChartComponent />
      </Suspense>
    </div>
  );
}

export default App;
```
```js
import React from 'react';

const ChartComponent = () => {
  return (
    <div>
      <h2>Chart Data</h2>
      {/* Chart rendering logic here */}
      <p>This is a complex chart component with significant JS size.</p>
    </div>
  );
};

export default ChartComponent;
```
---

### 6. Next.js basic concepts ?

- a popular framework built on top of React **that enables functionality such as `server-side rendering` and `static site generation`**, which are beneficial for performance and SEO. 


- #### Static Site Generation (SSG): 
    - Next.js supports generating a full static website using `getStaticProps` and `getStaticPaths`
    - These functions **allow you to <ins>fetch data at build time</ins>** and <ins>**render your HTML pages ahead of time**</ins>, which can be served directly from a CDN.


- #### Server-Side Rendering (SSR)
  - You can **render pages on the server** on a per-request basis using `getServerSideProps`. 
  - This is useful for fetching data per request and **doing operations that require server-side computation** or access to secure environments not suitable for the client-side.

- #### Image Optimization
  - The `Image` component from **next/image** is an extension of the HTML `<img>` element **designed for automatic image optimization**. 


-----

### 7. About common components ?
- Referred to `shared` or `re-usable` components
- Promoting `DRY` (Don't Repeat Yourself) principles and improving code maintainability and scalability.

```js
// RE-USABLE BUTTON COMPONENT
import React from 'react';

// Button component with customizable properties
const Button = ({ text, onClick, type = 'primary' }) => {
  const buttonStyle = type === 'primary' ? 'button-primary' : 'button-secondary';
  return (
    <button className={buttonStyle} onClick={onClick}>
      {text}
    </button>
  );
};

export default Button;
```

```js
//App.js
import React from 'react';
import Button from './Button';

const App = () => {
  return (
    <div>
      <Button text="Click Me" onClick={() => alert('Clicked!')} type="primary" />
      <Button text="Submit" onClick={() => alert('Submitted!')} type="secondary" />
    </div>
  );
};

export default App;
```
#### Benefits of Common Components:

- **Consistency**: 
  - Using the same components throughout an application ensures UI/UX consistency, which is crucial for user navigation and satisfaction.
- **Maintainability**: 
  - Updates or changes made in a common component propagate throughout the application wherever it is used. This makes maintenance easier and reduces the risk of bugs.
- **Scalability**: 
  - As applications grow, having a library of common components **can greatly simplify the process of scaling up**. 
  - New pages and features can be built more quickly by leveraging existing components.

----

### 8.  HOC and custom hooks implementation?


#### i) HOC:
- Higher-Order Components (HOCs) are a **pattern used in React to share common functionality between components without repeating code**. 
- An HOC is a function that takes a component and returns a new component.

```js
import React from 'react';

// This is the HOC
function withLoading(Component) {
  //The reason for naming the function EnhancedComponent when using a 
  // higher-order component (HOC) in React is primarily for clarity and better debugging. 
  // However, it's not strictly necessary to give the function a name, 
  // and you can indeed return an anonymous function.
  return function EnhancedComponent({ isLoading, ...props }) {
    if (isLoading) {
      return <div>Loading...</div>;
    }
    return <Component {...props} />;
  };
}

// Example usage of the HOC
function MyComponent({ data }) {
  return <div>Data: {data}</div>;
}

// EnhancedComponent will show a loading spinner when isLoading is true
const MyComponentWithLoading = withLoading(MyComponent);

export default MyComponentWithLoading;
```
```js
// in App.jsx
import React from 'react';
import MyComponentWithLoading from './MyComponentWithLoading'; // Assuming the export is set up

function App() {
  const [loading, setLoading] = React.useState(true);
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    setTimeout(() => {
      setData("Here's some data!");
      setLoading(false);
    }, 2000); // Simulate fetching data
  }, []);

  return (
    <div>
      <MyComponentWithLoading isLoading={loading} data={data} />
    </div>
  );
}

export default App;
```





----

#### ii) CUSTOM HOOKS:

```js
import { useState, useEffect } from 'react';

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchData() {
      try {
        const response = await fetch(url);
        const json = await response.json();
        setData(json);
        setLoading(false);
      } catch (error) {
        setError(error);
        setLoading(false);
      }
    }
    
    fetchData();
  }, [url]); // Only re-run the effect if url changes

  return { data, loading, error };
}

export default useFetch;
```

```js
// using the custom hook

import React from 'react';
import useFetch from './useFetch'; // Assuming useFetch is in a file named useFetch.js

function DataFetchingComponent({ url }) {
  const { data, loading, error } = useFetch(url);

  if (loading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  
  return <div>Data: {JSON.stringify(data)}</div>;
}

export default DataFetchingComponent;
```
-----

### 9.  Login screen design authentication and authorization.

#### 1. User Interface Design
- **Form Components**: Use `controlled components` in React for inputs to handle form data securely.
- **Responsiveness**: Ensure the login page is `responsive` using CSS frameworks like Bootstrap or TailwindCSS, or by using CSS Grid and Flexbox.
- **Feedback**: <ins>***Provide immediate input validation feedback***</ins> to enhance user experience (UX). 
  - Use libraries like `Formik` or `React Hook Form` to manage form state and validation.

#### 2. Authentication Process
- **API Integration**: 
  - Discuss how you would **connect the login form to backend services using Axios** to submit user credentials.
- **JWT (JSON Web Tokens)**: 
  - Explain the use of JWT **for maintaining user sessions**. 
  - Describe how the token is stored securely in the browser <ins>(e.g., using HttpOnly cookies or localStorage with proper security measures against XSS attacks).</ins>
- **Password Handling**: 
  - Mention the importance of **hashing passwords on the server side** and never transmitting or storing plain-text passwords.
  
#### 3. Security Considerations
- **HTTPS**: 
  - using HTTPS to secure data transmission between the client and the server.
- **CORS (Cross-Origin Resource Sharing)**: 
  - handle CORS in React by configuring the **server to accept requests from specific origins**.
- **CSRF (Cross-Site Request Forgery) Protection**: 
  - one strategy is using a**nti-CSRF tokens**.

#### 4. Authorization
- **Role-Based Access Control (RBAC)**: 
  - to manage user permissions and access levels within the application.
- **Protected Routes**: 
  - Use `React Router` for navigating protected or private routes that require authentication. 
  - Discuss how to redirect users to the login page if they are not authenticated.
- **Context API or Redux**: 
  - Any state management library like Redux **to manage global authentication state across all components**.

#### 5. Session Management
- **Token Expiry and Renewal**: 
  - Discuss handling token expiry, <ins>**including automatic renewal of tokens through refresh tokens**</ins> if implemented.
- **User Logout**: 
  - Ensure proper logout functionality <ins>**that clears the session and tokens securely from the client-side storage**</ins>.



#### 6. Error Handling
- **User Feedback**: 
  - Implement and explain robust error handling that provides clear, user-friendly error messages **for issues like network errors, wrong credentials, or server downtime**.
- **Try/Catch**: 
  - Use try/catch blocks in asynchronous actions to handle exceptions and errors gracefully.


#### 7. Testing and Best Practices
- **Unit Testing**: 
  - Talk about using `Jest` and `React Testing Library` to write unit tests for components and hooks.
- **End-to-End Testing**: 
  - Mention tools like `Cypress` or `Selenium` for end-to-end testing of the authentication flow.
- **Code Quality**: 
  - Discuss the importance of coding best practices such as linting with ESLint, formatting with Prettier, and following secure coding guidelines.


```js
//api.js
import axios from 'axios';

const API_URL = 'https://your-api-url.com/api';

export const loginUser = async (credentials) => {
  try {
    const response = await axios.post(`${API_URL}/login`, credentials);
    return response.data; // This should include the JWT
  } catch (error) {
    console.error('Login error', error.response);
    throw error.response.data;
  }
};
```
```js
//authContext.js
import React, { createContext, useContext, useState, useEffect } from 'react';
import jwtDecode from 'jwt-decode'; // npm install jwt-decode

const AuthContext = createContext(null);

export const AuthProvider = ({ children }) => {
  const [authData, setAuthData] = useState(() => {
    const token = localStorage.getItem('token');
    if (token) {
      const decoded = jwtDecode(token);
      if (decoded.exp * 1000 > Date.now()) {
        return { user: decoded };
      }
    }
    return null;
  });

  const login = (data) => {
    localStorage.setItem('token', data.token);
    setAuthData({ user: jwtDecode(data.token) });
  };

  const logout = () => {
    localStorage.removeItem('token');
    setAuthData(null);
  };

  useEffect(() => {
    const token = localStorage.getItem('token');
    if (token) {
      const decoded = jwtDecode(token);
      if (decoded.exp * 1000 <= Date.now()) {
        logout();
      }
    }
  }, []);

  return (
    <AuthContext.Provider value={{ authData, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => useContext(AuthContext);
```

```js
//Login.js
import React, { useState } from 'react';
import { useAuth } from './AuthContext';
import { loginUser } from './api';

const Login = () => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');
  const { login } = useAuth();

  const handleSubmit = async (event) => {
    event.preventDefault();
    try {
      const data = await loginUser({ username, password });
      login(data);
    } catch (error) {
      setError(error.message);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>Username:</label>
        <input type="text" value={username} onChange={(e) => setUsername(e.target.value)} />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} />
      </div>
      <button type="submit">Login</button>
      {error && <p>{error}</p>}
    </form>
  );
};

export default Login;
```

```js
//PrivateRoute.js
import React from 'react';
import { Route, Redirect } from 'react-router-dom';
import { useAuth } from './AuthContext';

const PrivateRoute = ({ component: Component, roles, ...rest }) => {
  const { authData } = useAuth();

  return (
    <Route
      {...rest}
      //In the above, `...rest` could include props like 
      // `path`, `exact`, `strict`, `location`, `sensitive`, etc., 
      // which are valid `<Route>`props but are not directly 
      // used in your logic before passing them to <Route>.
      render={(props) => {
        // This props object includes several properties such as: `match`, `location`, `history`
        if (!authData) {
          // Not logged in
          return <Redirect to="/login" />;
        }

        if (roles && !roles.includes(authData.user.role)) {
          // Role not authorized
          return <Redirect to="/unauthorized" />;
        }

        return <Component {...props} />;
      }}
    />
  );
};

export default PrivateRoute;
```

```js
//App.jsx
import React from 'react';
import { BrowserRouter as Router, Route, Switch, Redirect } from 'react-router-dom';
import Login from './Login';
import Dashboard from './Dashboard';
import AdminPanel from './AdminPanel';
import PrivateRoute from './PrivateRoute';  // Imported PrivateRoute

const App = () => {
  return (
    <Router>
      <Switch>
        <Route path="/login" component={Login} />
        <PrivateRoute path="/dashboard" component={Dashboard} />
        <PrivateRoute path="/admin" component={AdminPanel} roles={['admin']} />
        <Redirect from="/" to="/dashboard" />
      </Switch>
    </Router>
  );
};

export default App;
```

------

### 10. Promises.

#### i) Why Promises?
- Promises in JavaScript are a powerful tool **for managing <ins>asynchronous operations</ins>**.

#### ii) What problems does Promises solve?

- Provide a **cleaner, more robust <ins>alternative**</ins> to older techniques like <ins>**callbacks and events**</ins> for handling asynchronous tasks such as network requests, file operations, or timers

#### Definition
- A Promise in JavaScript **is an object** <ins>representing the eventual ***completion (or failure)*** of an asynchronous operation</ins>. 
- It essentially <ins>**promises to give you a result at some point in the future**</ins>, either a successful result or a reason for its failure.

#### States of a Promise
- A Promise has three states:

  - **Pending**: Initial state, neither fulfilled nor rejected.
  - **Fulfilled**: The operation completed successfully.
  - **Rejected**: The operation failed.

#### Creating a Promise

```js
const myPromise = new Promise((resolve, reject) => {
    if (true) {
        resolve('Promise is fulfilled successfully!');
    } else {
        reject('Promise was rejected!');
    }
});
```

```js
// Consuming a Promise
// To handle the results of a promise, 
// you can use the .then() and .catch() methods.

.then()
.catch()
```

#### Chaining Promises
- Promises can be chained **to perform a sequence of asynchronous operations <ins>where each subsequent operation starts when the previous one is successful, and its result becomes the input for the next</ins>**.

```js
new Promise((resolve, reject) => {
    setTimeout(() => resolve(1), 1000); // Simulate async operation
})
.then(result => {
    console.log(result); // 1
    return result * 2;
})
.then(result => {
    console.log(result); // 2
    return result * 2;
})
.then(result => {
    console.log(result); // 4
    return result * 2;
});
```

#### Error Handling:

```js
new Promise((resolve, reject) => {
    throw new Error('Something failed!');
})
.then(result => {
    // This won't be called
})
.catch(error => {
    console.error(error.message); // "Something failed!"
});

```

----

1.  Normalization techniques in database.
2.  About Micro-frontend and it Pros, cons, communication between MFE, sharing common component between MFE, Design Question
3.  About SOLID principles.
4.  How to Implement offers in the E-commerce sites
5.   useEffect 
    - explain how we achieve different lifecycle
    - Behavior with different dependency array - null, [], [value]
6.  useRef vs forwardRef
7.  useContext with example, useReducer with example
8.   Typescript questions
9.   what is sass and how good you are in it
10.  I have service which will give data of an employee and hierarchy, we need to display that data in ui exactly like teams organization structure, how you will achieve that?