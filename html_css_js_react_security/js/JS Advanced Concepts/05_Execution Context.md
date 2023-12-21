### 5. Execution Context:

- Whenever our code run in Javascript, it is run inside an Execution Context. (This might be of Global or Inside function that we call).

- The base execution context that runs is called **Global Execution Context**

- Initially our Javascript engine is going to create a global execution context and on top of that we start adding the functions (ex: sayMyName()) in our case.

- And as the execution context(s) gets popped off, the last thing that remains is Global Execution context. And when the final line of our code runs and we're done with the JS engine, this GEC is going to be popped off.

- Whenever the Javascript engine sees `those brackets`, **_it's going to run a function and create execution context_**.

- So first thing it does it creates the execution context sayMyName() and adds this execution context onto the Call Stack
- And then it tries to run the function and **sees that this function is calling another function**. **_So a new execution context is now created_** for findMyName
- Now the Javascript engine comes across another function called printName for which it creates a new execution context.

- the Last function after creating its own execution context (printName()), it returns the string output and this gets returned to findMyName function and this gets returned to sayMyName function and then eventually call stack gets popped off and we return onto the screen the string output.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/821daceb-6a17-4bc5-bdf2-930d4dd7dd6a)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/6c0ecf64-5d4f-439e-a769-1edccba0537b)

##### <u>Global Execution Context:</u>

- After creating GEC, JS engines creates two things.
- First thing is **_global object_**, and the other thing is **_this keyword_** in Javascript.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/f0037f7f-1074-4c72-8d00-6688ebb320a5)

**_Global Object means Window_**
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/4c5fa03e-f081-4dd2-98a0-436ef09db2be)

- We can add variables/functions and many more to our global object (e.g. let a = "saiteja" will be part of window.a)

- So the above is called **_creation phase_**
- The second phase is called as **_execution phase._** (Where you actually run your code)

##### <u>Note:</u> If you're using Node, the global object wouldn't be window, instead it would be called `global`
