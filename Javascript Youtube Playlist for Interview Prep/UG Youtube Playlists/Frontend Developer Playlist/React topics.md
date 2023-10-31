### Pure Component

- React.PureComponent is similar to the React.Component.

- The difference between them is that React.Component doesn't implement shouldComponentUpdate() but React.PureComponent() implements it with a shallow prop and state comparison

- Pure components re-renders only when state or props passed are changed.

- Your Pure component should be wrapped with React.memo

- As long as the Pure component props are not changed then Pure component won't re-render.
