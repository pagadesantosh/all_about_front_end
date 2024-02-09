**React Compound Pattern**

- Multiple components come together to serve a common functionality
- Ex: Select tag where select and option jointly help us create dropdowns.
- React Context APIs plays an important role in Compound pattern
- Use cases like: select, dropdown components, menu items

```js
//App.js
import { useState } from 'react';
import './styles.css';
import Tab from './Tab';
export default function App() {
  const [currentIndex, setIndex] = useState(0);

  const handleChange = (newIndex) => {
    setIndex(newIndex);
  };
  return (
    <div className='App'>
      <Tab value={currentIndex} onChange={handleChange}>
        <Tab.Heads>
          <Tab.Item label={'Tab1'} index={0} />
          <Tab.Item label={'Tab2'} index={1} />
          <Tab.Item label={'Tab3'} index={2} />
        </Tab.Heads>
        <Tab.ContentWrapper>
          <Tab.Content index={0}>
            <h1>I am content 1</h1>
          </Tab.Content>
          <Tab.Content index={1}>
            <h1>I am content 2</h1>
          </Tab.Content>
          <Tab.Content index={2}>
            <h1>I am content 3</h1>
          </Tab.Content>
        </Tab.ContentWrapper>
      </Tab>
    </div>
  );
}
```

```js
//Tab.js
import { createContext, useContext } from 'react';
import './Tab.css';
const TabContext = createContext();

export default function Tab({ children, value, onChange }) {
  return (
    <div>
      <TabContext.Provider value={{ value, onChange }}>
        {children}
      </TabContext.Provider>
    </div>
  );
}
Tab.Heads = ({ children }) => {
  return <div className='heads'>{children}</div>;
};

Tab.Item = ({ label, index, children }) => {
  const { value, onChange } = useContext(TabContext);
  const handleClick = () => {
    onChange(index);
  };
  return (
    <div
      onClick={handleClick}
      className={`item ${index === value ? 'active' : null}`}
    >
      {label}
    </div>
  );
};

Tab.ContentWrapper = ({ children }) => {
  return <div className='contentWraper'>{children}</div>;
};

Tab.Content = ({ children, index }) => {
  const { value } = useContext(TabContext);
  return value === index ? <div>{children}</div> : null;
};
```

```js
.heads {
  border-radius: 5px;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
}

.item {
  background-color: red;
  color: white;
  padding: 10px;
  width: 100%;
  cursor: pointer;
}

.item.active {
  background-color: brown;
}

.contentWraper {
  background-color: grey;
  margin: 0;
  padding: 10px;
}
```
