### Fragments

- Fragments <u>**_allows to group a list_**</u> of children without adding extra nodes to the DOM

```js
function ComponentA(){
    return(
        <React.Fragment>
        <ComponentB>
        <ComponentC>
        <ComponentD>
        </React.Fragment>
    )
}
```
#### Benefits: 
- A bit faster and has less memory usage (no need to create an extra DOM node).
- You would only see a real benefit on very large and or deep trees.
- DOM inspector is less cluttered.