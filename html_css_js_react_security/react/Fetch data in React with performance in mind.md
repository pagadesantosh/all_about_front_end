- if you have a case saying like <strong>fetch once and forget</strong> then use fetch instead of external libraries like axios to call the api.

- But it leads to lot of differnt questions like

1. What about error handling ?
2. What if multiple components want to fetch data from this exact endpoint ?
3. Do I need to cache the data ? If yes, for how long?
4. What about race conditions?
5. What if I want to remove the component from the screen ? Should I cancel the request?
6. What about memory leaks?

- Not even a single question is related to React but it's a general problem of fetching the data over the network.

- Libraries like axios will abstract some concerns like cancelling requests.

##### Let's take a real world example

- If a app is implemented in three differnt ways

1. Shows a loading state until all the data is loaded and then renders everything at a go. Assuming it takes ~3 seconds

2. Shows a loading state until sidebar data is loaded first, renders sidebar and keeps the loading state until the data is finished in the main part. (sidebar takes ~1 second, main part takes ~3 seconds). Total is 4 seconds

3. Shows a loading state until main data is loaded, renders it, keeps loading state for sidebar and comments. When sidebar loaded, rendes it, whereas comments are still in loading state. Main part takes ~2 seconds, sidebar ~1 second and after that, takes another ~2 seconds for comments. Overall ~5 seconds to appear.

- We cannot conclude which is the best performant app due to various scenarios.. It always depends on the message you're trying to convey to the users.

##### When it is okay to start fetching data ?

##### what can we do while the data fetching is in the progress ?

##### what should we do when the data fetching is done?

#### So before jumping to the actual techniques, we need to understand two more very fundamental things:

1. React Lifecycle and data fetching

- When React component's lifecycle should be triggered is the most important thing to know and remember

```js
// Only after Parent's isLoading state changes to false, then child component rendering and other effects will be triggered.

const Child = () => {
  useEffect(() => {
    // do something here, like fetching data for the Child
  }, []);

  return <div>Some child</div>;
};

const Parent = () => {
  // set loading to true initially
  const [isLoading, setIsLoading] = useState(true);

  if (isLoading) return "loading";

  return <Child />;
};
```

```js
// Only after Parent's isLoading state changes to false, then child component rendering and other effects will be triggered.

const Child = () => {
  useEffect(() => {
    // do something here, like fetching data for the Child
  }, []);

  return <div>Some child</div>;
};

const Parent = () => {
  // set loading to true initially
  const [isLoading, setIsLoading] = useState(true);

  // this won't trigger the useEffect until the child is returned i.e  It only is rendered when returned from the component.

  const child = <Child />;

  if (isLoading) return "loading";

  return child;
};
```
This article might be interesting to read:
https://www.developerway.com/posts/react-elements-children-parents