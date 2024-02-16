### React HOC Pattern (Higher Order Component)

#### What is HOC ?

- **_Higher Order Component <u>receives a component</u>_**, applies a certain logic and **_<u>then return that component with those additional logics</u>_**

#### When to use HOC?

- When we want **_<u>to apply same logic to multiple components</u>_**

```js
// Component1.jsx
import React from 'react';

const Component1 = () => <div>Hello from Component 1</div>;

export default Component1;
```

```js
// Component2.jsx
import React from 'react';

const Component2 = () => <div>Welcome to Component 2</div>;

export default Component2;
```

```js
// withAuthorization.jsx
import React from 'react';
import { Redirect } from 'react-router-dom';

const withAuthorization = (WrappedComponent) => {
  return function (props) {
    const { isLoggedIn } = props;
    if (!isLoggedIn) {
      return <Redirect to='/login' />;
    }
    return <WrappedComponent {...props} />;
  };
};

export default withAuthorization;
```

```js
// App.jsx
import React, { useState } from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';

//import your components + HOC Component
import withAuthorization from './withAuthorization';
import Component1 from './Component1';
import Component2 from './Component2';

// Components wrapped with HOC
const AuthComponent1 = withAuthorization(Component1);
const AuthComponent2 = withAuthorization(Component2);

const Login = ({ onLogin }) => (
  <div>
    <button onClick={onLogin}>Log in</button>
  </div>
);

const App = () => {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  const handleLogin = () => setIsLoggedIn(true);

  return (
    <Router>
      <div>
        <Routes>
          <Route path='/login'>
            <Login onLogin={handleLogin} />
          </Route>
          <Route path='/component1'>
            <AuthComponent1 isLoggedIn={isLoggedIn} />
          </Route>
          <Route path='/component2'>
            <AuthComponent2 isLoggedIn={isLoggedIn} />
          </Route>
        </Routes>
      </div>
    </Router>
  );
};

export default App;
```
