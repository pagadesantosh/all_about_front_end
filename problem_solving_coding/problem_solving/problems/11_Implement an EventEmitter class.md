## Implement an EventEmitter class

<strong>Approach Taken:</strong>

1. this.events is an object inside constructor function
2. on, off receives eventName and callback as arguments and we check eventName is present or not in the this.events object ex: this.events[eventName]
3. for `on` method, if there is no eventName then create an array ex: this.events[eventName] = [] and push the callback (2nd arg) inside array
4. off is to filter inside, emit is to loop inside

```js
class EventEmitter {
  constructor() {
    // Object to manage events and callbacks
    this.events = {};
  }

  // Register an event with a callback
  on(eventName, callback) {
    if (!this.events[eventName]) {
      this.events[eventName] = [];
    }
    this.events[eventName].push(callback);
  }

  // Trigger an event
  emit(eventName, ...args) {
    if (this.events[eventName]) {
      this.events[eventName].forEach((callback) => {
        callback(...args);
      });
    }
  }

  // Remove a specific callback for an event
  off(eventName, callback) {
    if (this.events[eventName]) {
      this.events[eventName] = this.events[eventName].filter(
        (cb) => cb !== callback
      );
    }
  }

  // Remove all callbacks for an event
  removeAllListeners(eventName) {
    if (this.events[eventName]) {
      delete this.events[eventName];
    }
  }
}

// Example usage:
const emitter = new EventEmitter();
emitter.on('data', (data) => {
  console.log('Received data:', data);
});
emitter.on('userJoined', (...usernames) => {
  usernames.forEach((userName) => {
    console.log(`${userName} has joined the chat.`);
  });
});

emitter.emit('data', { test: 123 }); // Outputs: Received data: { test: 123 }
emitter.emit('userJoined', 'Alice', 'Blice', 'Clice');
// Outputs:
// Alice has joined the chat.
// Blice has joined the chat.
// Clice has joined the chat.
```
