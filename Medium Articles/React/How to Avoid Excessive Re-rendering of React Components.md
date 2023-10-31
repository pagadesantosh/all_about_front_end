##### 1. Always use the key while mapping (don't use index as a key)

```js
// never do this, it is a bad idea due to specific React library

list.map((item, index) => {
  return <div key={index}>Hello</div>;
});
```

---

#### 2. Pay attention to the nesting of elements and their types

#### 3. Selectors and Redux

- Every time the dispatch of a action occurs modifying the state of the Redux Store, the corresponding useSelector will be called.
- It is essential to understand that if the useSelector returns an object or an array. (If the references differ then re-render will be performed)

##### Wrong way

```js
export const selectTagsByProductId = (state, id) =>
  state.product[id].tags || [];
```

##### Right way

```js
const EMPTY_ARRAY = Immutable([]);

export const selectTagsByProductId = (state, id) =>
  state.product[id].tags || EMPTY_ARRAY;
```

##### Redux in its official documentation, recommends the following optimization methods

1. Return Scalar data types (string, number, boolean, undefined)
2. Use libraries like reselect or similar
3. Use the shallowEqual function from the 'react-redux' package as the second argument

```js
// Typical example of reselect usage
const selectUserTagById = (state, userId) => state.user[userId].tag;

const selectPictures = (state) => state.picture;

const selectRelatedPictureIds = createSelector(
  [selectUserTagById, selectPictures],
  (tag, pictures) =>
    Object.values(pictures)
      .filter((picture) => picture.tags.includes(tag))
      .map((picture) => picture.id)
);
```

- reselect understands on when to take from cache and when to recalculate based on the shallowEqual

- Ex: if the selector arguments have not changed
- Ex: if the results of inputSelectors have not changed

---

#### 4. Memoisation

1. React.memo

- React.memo caches the component and re-renders only if the properties have been changed.
- It's important to understand that reference will affect the rendering (when a new value comes for the component each time). In this case there will be no benefit to use memoization at all.

```js
const MemoizedComponent = React.memo((props) => (
  <SomeComponent props={props} />
));
```

2. React.useCallback

- It returns a new function if something in the dependencyList changes. Otherwise it produces the reference to the function in memory, which will return true(due to comparing prevProps vs nextProps).

- useCallback is only needed to check references.
- Don't use useCallback for native DOM element as it don't compare references.

```js
const onClick = useCallback(callbackFunc, dependencyList);
```

3. React.useMemo

- Works same as useCallback but don't forget to add the second argument which is dependency array

```js
const filteredArrary = useMemo(() => someExpensiveFunction(), dependencyList);
```

###### However, it’s important to remember that these hooks work effectively only together with memoised components, but not separately.

---

#### Reference to medium article:

https://medium.com/@ownger/how-to-avoid-excessive-re-rendering-of-react-components-c6b9a5f0c722
