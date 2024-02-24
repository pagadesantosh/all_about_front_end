### 2. Call Stack and Memory Heap

#### <u>Call stack:</u>

- Place to **keep track of where we are in the code** so that we can run the code in order.
- Call Stack operates in **LIFO Mode (Last In First Out)**
- Call Stack stores functions and variables as your code executes at each entry of the stack helps us to know where we are in the code

#### <u>Memory Heap:</u>

- We need memory heap **as a place to store and write information**.
- That is the reason we have a place for allocating memory, use memory and release memory.
- There is no order in storing data.

##### <u>Animation:</u>
![alt text](<images used/Call Stack.png>)

##### <u>Example Scenario:</u>
![alt text](<images used/CallStack memory allocation.png>)

##### <u>Below shows us how Call Stack work behind the scenes:</u>

<i>Below is the code:</i>
![alt text](<images used/CallStack behind the scenes.png>)

**Global Execution Context**: (anonymous)
![alt text](<images used/Global Execution Context.png>)

**After calculate() function is invoked**, it is added to the top of the Call Stack
![alt text](<images used/Function invocation added to callstack.png>)

**After subtractTwo() function is invoked**, it is added to the top of the call stack
![alt text](<images used/Function invocation added to callstack-1.png>)

**Note:** We can get Maximum call stack size exceeded in one of the scenarios like **Recursion** which means a function calling itself
![alt text](<images used/Maximum call stack exceeded.png>)