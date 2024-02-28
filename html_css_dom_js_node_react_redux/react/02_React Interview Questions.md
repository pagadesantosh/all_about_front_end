1. Can you explain the virtual DOM and its role in React?💯

18. **`Shadow DOM vs. Virtual DOM`**: What are the differences and use cases?

<details>
<summary>View Answer</summary>

_Shadow Dom_:

- offers encapsulation for DOM and CSS. It allows for the creation of a separate DOM tree with its styles and scripts which is attached to an element but doesn't interfere with the main Document's DOM.

_Uses_: Shadow DOM is used when you want to create reusable and isolated components.

- It's beneficial for widget development, plugins or any scenario where you don't want your component's internals to clash with the surrounding environment.
- Since the Shadow DOM is isolated from the main document, **changes made inside a shadow tree do not directly affect the main document's DOM**.

```js
const element = document.getElementById('myElement');
const shadowRoot = element.attachShadow({ mode: 'open' });
shadowRoot.innerHTML = `<style>p { color: red; }</style><p>Hello, Shadow DOM!</p>`;
```

_Virtual Dom_:

- Is Virtual representation of a UI kept in memory and synced with the `real DOM` through a process called reconciliation. Technique popular in React

**Differences:** Virtual DOM provides a way to update the view in a more optimized and efficient manner. Instead of making direct changes to the real DOM (which can be slow) changes are made to the virtual DOM, which then calculates the diff between the current and the new state and updates the real DOM in a minimal way.

**Not Native**: Virtual DOM is not a web standard. It's a technique used by specific libraries and frameworks

**Use Cases**: Virtual DOM is beneficial in scenarios where frequent updates to the UI can lead to the performance bottlenecks. Virtual DOM ensures a smoother User Experience.

**Summary**:

_Shadow DOM_: is about encapsulation, isolating components and their styles/scripts from the main document to prevent conflicts and leaks

_V Dom_: is about performance: optimizing the way the UI updates by minimizing direct interactions with the real DOM.

- If you're building a reusable widget or component that you want to remain isolated from the surrounding env, consider using Shadow DOM.

- If you're developing a dynamic web app where the UI changes frequently and you want to optimized those updates, consider using a library or framework that employs VDom like React.

</details>




2. How does React handle event handling?
3. How can we handle errors in React?🔥
4. How does React handle component state and props?
5. What is JSX?⭕
6. Explain the component lifecycle.🔥🔥
7. How to Use map() method in Reactjs.💯
8. Explain Difference between map(), filter(),reduce() method. 🔥
9.  Tell me the component uses in the component lifecycle.
10. How do you optimize the performance of a React application? 💯
11. Explain React Router works.💯
12. What is Redux? Explain how it works and its benefits.💯
13. Explain “controlled” and “uncontrolled” components. 🔴
14. Have you ever used React Hooks? If Yes, Give an example of a Hook you have used and explain its purpose.🔴🔴
15. Can you explain the difference between a Presentational and Container component in React?
16. Have you ever worked with any CSS library in Reactjs? Give Its Names.
17. Can you explain the difference between server-side rendering and client-side rendering in React?
18. Explain how React handles server-side rendering (SSR)?🔴
19. What are Props?⭕
20. What are Props drilling?
21. How to Overcoming Props drilling?
22. Can you explain the Higher Order Components (HOC) concept in React?
23. Have you ever worked with Webpack or other build tools in a React project? If so, can you explain how you configured it?
24. Explain UseEffect(), UseCallback(), and UseMemo() and what is Difference Between them.💯
25. Explain UseContext().💯
26. Have you ever worked with GraphQL in a React project? If so, can you give an example of a query or mutation you have implemented?
27. Explain how React handles forms and form validation.💯
28. Can you explain the concept of “reconciliation” in React?
29. Have you ever worked with any other libraries or frameworks for accessibility in React? If so, which ones and why?
30. Can you explain the concept of “forwarding refs” in React?🔴
31. Can you explain how React handles server-side rendering with a Node.js backend? 🔥
