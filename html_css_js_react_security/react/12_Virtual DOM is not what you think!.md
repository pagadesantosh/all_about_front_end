### Virtual DOM is not what you are thinking!

- The virtual DOM is only a virtual representation of the DOM.
- Every time the state of our application changes, the **_virtual DOM gets updated_** instead of the real DOM.

<u>**Points to remember**</u>:

- When **new elements are added** to the UI, a **virtual DOM**, which is represented as a tree **_is created_**.

- <u> **If the state of any of these elements changes, a new virtual DOM tree is created.**</u>

- This tree is then compared or “diffed” with the previous virtual DOM tree.

- Once this is done, the virtual DOM calculates the best possible method to make these changes to the real DOM.

**Pros of Virtual DOM**:

- Updates process is optimized and accelerated.
- Virtual DOM is ideal for mobile first applications.
- Prompt rendering. Using comprises methods to minimize number of DOM operations helps to optimize updating process and accelerate it.

<img src="https://github.com/krishnakiriti04/react-interview-questions/raw/master/assets/dom.png">
