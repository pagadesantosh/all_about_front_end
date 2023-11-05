**API URL**:

```js
https://openlibrary.org/search.json?q=spy&page=1
```

```js
//App.js
import React, { useState } from 'react';
import { useCallback } from 'react';
import InfiniteScroll from './InfiniteScroll';
import { useRef } from 'react';
function App() {
  const [query, setQuery] = useState('');
  const [data, setData] = useState([]);
  const controllerRef = useRef(null);

  //onChange of search input box
  const handleInput = useCallback((e) => {
    setQuery(e.target.value);
  }, []);

  //render HTML
  const renderListItem = useCallback(({ title }, key, ref) => (
    <div ref={ref} key={key}>
      {title}
    </div>
  ));

  // api call
  const getData = useCallback((query, pageNumber) => {
    return new Promise(async (resolve, reject) => {
      try {
        //abort is used to cancel the previous requests
        if (controllerRef.current) controllerRef.current.abort();
        controllerRef.current = new AbortController();
        const promise = await fetch(
          'https://openlibrary.org/search.json?' +
            new URLSearchParams({
              q: query,
              page: pageNumber,
            }),
          { signal: controllerRef.current.signal }
        );
        const data = await promise.json();
        console.log(data);
        resolve();
        setData((prevData) => [...prevData, ...data.docs]);
      } catch (error) {
        reject();
      }
    });
  }, []);

  return (
    <>
      <input type='text' onChange={handleInput} value={query} />
      <InfiniteScroll
        renderListItem={renderListItem}
        getData={getData}
        listData={data}
        query={query}
      />
    </>
  );
}

export default App;
```

```js
//InfiniteScroll.js
import React from 'react';
import { useCallback } from 'react';
import { useState } from 'react';
import { useRef } from 'react';
import { useEffect } from 'react';

const InfiniteScroll = (props) => {
  const { renderListItem, getData, listData, query } = props;
  const pageNumber = useRef(1);
  const [loading, setLoading] = useState(false);
  const observerRef = useRef(null);

  const fetchData = useCallback(() => {
    setLoading(true);
    getData(query, pageNumber.current).finally(() => {
      setLoading(false);
    });
  }, [query]);

  useEffect(() => {
    fetchData();
  }, [fetchData]);

  //logic for Infinite scrolling
  const lastElementObserver = useCallback((node) => {
    if (loading) return;
    if (observerRef.current) {
      observerRef.current.disconnect();
    }
    observerRef.current = new IntersectionObserver((entries) => {
      if (entries[0].isIntersecting) {
        pageNumber.current += 1;
        fetchData();
      }
    });
    //important line
    if (node) {
      observerRef.current.observe(node);
    }
  });

  const renderList = useCallback(() => {
    return listData.map((item, index) => {
      //if item is the lastElement, the ref is lastElementObserver
      if (index === listData.length - 1) {
        return renderListItem(item, index, lastElementObserver);
      }
      //if item is not the lastElement, the ref is null
      return renderListItem(item, index, null);
    });
  });

  return (
    <div>
      {renderList()}
      {loading && <h4>Loading...</h4>}
    </div>
  );
};

export default InfiniteScroll;
```
