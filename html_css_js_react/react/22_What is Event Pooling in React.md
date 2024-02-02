### Event Pooling in React

- They SyntheticEvent is pooled.
- This means that the SyntheticEvent object will be reused and **_all properties will be nullified after the event callback has been invoked_**.

<u>**Points to remember:**</u>

- You cannot access the event in an asynchronous way
- **If we want to access the event properties in an asynchronous way**, <u>we should call event.persist() on the event</u>,
- By doing above <u>**_will remove the synthetic event from the pool_**</u> and allow references to the event to be retained by user code.
