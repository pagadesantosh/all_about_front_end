### 3. Garbage Collection:

- Javascript is a **garbage collected** language
- That means when Javascript allocates memory
  (e.g. within a function, we create an object and that objects gets stored somewhere in our memory heap. Automatically with javascript **when we finish calling the function** and **if we don't need that object anymore**, `it's going to be garbage collected`)
- So Javascript **_automatically frees up this memory_** that we no longer use and well collect our garbage.
- Garbage collector frees up the memory and prevents from Memory leaks
- Garbage collection in javascript actually works on algorithm called **_Mark & Sweep_**

#### Imagine the left ones are the variables and these variables point to different objects

- In the below picture, Object 5 and Object 7, 8 are not being referenced to any,
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/382bb65d-7c47-454e-9a23-8a922c86af46)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/d5b0b905-da9a-4575-9414-222854880e58)
