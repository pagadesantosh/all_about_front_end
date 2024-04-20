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
1. Write HTML to display cards side by side ?
2. useMemo vs. useCallback ?
3. About React.lazy?
4. Next.js basic concepts ?
5. About common components ?
6. About performance loading ?
7.  HOC and custom hooks implementation?
8.  Login screen design authentication and authorization.
9.  Promises.
10. Normalization techniques in database.
11. About Micro-frontend and it Pros, cons, communication between MFE, sharing common component between MFE, Design Question
12. About SOLID principles.
13. How to Implement offers in the E-commerce sites
14.  useEffect 
    - explain how we achieve different lifecycle
    - Behavior with different dependency array - null, [], [value]
15. useRef vs forwardRef
16. useContext with example, useReducer with example
17.  Typescript questions
18.  what is sass and how good you are in it
19.  I have service which will give data of an employee and hierarchy, we need to display that data in ui exactly like teams organization structure, how you will achieve that?