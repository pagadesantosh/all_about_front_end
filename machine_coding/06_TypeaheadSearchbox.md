```js
//App.js
import './styles.css';
import SearchBox from './searchBox';
import ListBox from './listBox';
const maxItems = 5;
export default function App() {
  const transformData = (data) => data.results.slice(0, maxItems);
  const dataPromise = async (query, signal) =>
    await fetch(`https://swapi.dev/api/people/?search=${query}`, { signal });
  return (
    <div className='wrapper'>
      <SearchBox
        id='personName'
        name='personName'
        label='Enter Person Name'
        placeholder='Enter your fav star war char'
        autoComplete
        styles={{
          label: 'label',
          input: 'input',
        }}
        debounceWait={400}
        listBox={(items, activeIndex) => (
          <ListBox items={items} activeIndex={activeIndex} />
        )}
        noItemMessage={() => <div>Sorry no person found</div>}
        errorMessage={() => <div>Something went wrong</div>}
        transformData={transformData}
        promise={dataPromise}
      />
    </div>
  );
}
```

```js
//listBox.js
import './listBox.css';
const ListBox = ({ items, activeIndex }) => {
  return (
    <ul className='listBoxContainer'>
      {items.map((item, index) => (
        <li
          className={`listBoxItem ${index === activeIndex ? 'activeItem' : ''}`}
          key={index}
        >
          {item.name}
        </li>
      ))}
    </ul>
  );
};

export default ListBox;
```

```js
//searchBox/index.js
import { useState } from 'react';
import useFetchPromise from './useFetchPromise';
const SearchBox = ({
  id,
  name,
  label,
  placeholder,
  autoComplete,
  styles,
  debounceWait,
  listBox,
  noItemMessage,
  errorMessage,
  transformData,
  promise,
}) => {
  const [query, setQuery] = useState('');
  const [isAutoComplete, setIsAutoComplete] = useState(autoComplete);
  const [activeIndex, setActiveIndex] = useState(null);
  const [data, setData, error] = useFetchPromise(
    query,
    transformData,
    promise,
    debounceWait,
    isAutoComplete
  );
  const handleChange = (event) => {
    setQuery(event.target.value);
  };

  const handleKeyUp = (event) => {
    const keyCode = event.keyCode;
    if (keyCode === 13) {
      // user enter
      if (activeIndex === null) return;
      console.log(data[activeIndex].name);
      setQuery(data[activeIndex].name);
      setData(null);
      setActiveIndex(null);
      setIsAutoComplete(false);
      return;
    }
    setIsAutoComplete(true);
    if (!data || data.length === 0) return;
    if (keyCode === 40) {
      // move down
      if (activeIndex === null || activeIndex === data.length - 1) {
        setActiveIndex(0);
      } else {
        setActiveIndex((prevIndex) => prevIndex + 1);
      }
    } else if (keyCode === 38) {
      // move up
      if (activeIndex === 0) setActiveIndex(data.length - 1);
      else setActiveIndex((prevIndex) => prevIndex - 1);
    }
  };
  return (
    <>
      <label className={styles.label} for={name}>
        {label}
      </label>
      <br />
      <input
        name={name}
        className={styles.input}
        id={id}
        value={query}
        onChange={handleChange}
        placeholder={placeholder}
        autoComplete='off'
        onKeyUp={handleKeyUp}
      />
      {data && data.length > 0 && listBox(data, activeIndex)}
      {query && data && data.length === 0 && noItemMessage()}
      {error && errorMessage()}
    </>
  );
};

export default SearchBox;
```

````js
//searchBox/useFetchPromise.js
import { useEffect, useState, useCallback } from "react";
import debounce from "lodash/debounce";

const useFetchPromise = (
  query,
  transformData,
  promise,
  debounceWait,
  autoComplete
) => {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);

  const fetchData = useCallback(
    debounce(async (query, transformData, signal) => {
      try {
        const response = await promise(query, signal);
        if (!response.ok) throw new Error(response.statusText);
        const data = await response.json();
        console.log(data);
        setData(transformData(data));
      } catch (e) {
        console.log(e);
        if (!signal.aborted) setError(e);
      }
    }, debounceWait),
    []
  );

  useEffect(() => {
    if (!query || !autoComplete) {
      setData(null);
      setError(null);
      return;
    }
    const controller = new AbortController();
    const signal = controller.signal;

    fetchData(query, transformData, signal);

    return () => {
      controller.abort();
    };
  }, [query, transformData, fetchData, autoComplete]);

  return [data, setData, error];
};

export default useFetchPromise;
```
````

```js
//listBox.css

.listBoxContainer {
  margin: 0;
  padding: 0;
  list-style: none;
  width: 320px;
  border-radius: 10px;
  overflow: hidden;
}

.listBoxItem {
  background-color: black;
  color: white;
  padding: 10px;
  border-bottom: 1px solid white;
}

.activeItem {
  background-color: #d4cdcd;
  color: black;
}

```
