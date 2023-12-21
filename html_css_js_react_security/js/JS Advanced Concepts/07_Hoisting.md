### 7. Hoisting

- By Hoisting it means the **_behavior of moving the variables or function declarations to the top_**.

- During compilation phase, **_variables are partially hoisted_** and **_function declarations are hoisted_**. Variables declared with `var keyword` if logged before initialized will return **_undefined_**.

- Whenever JS engine **sees the var and function keywords** in the code, they are hoisted and JS engine **_allocates some memory_**.

- As we have two phases (creation phase and execution phase), we have **_Hoisting in the creation phase_**.

- White line divides creation phase and execution phase

##### <u>Refer below screenshot:</u>

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/3f31cc53-ff18-458c-b939-f00d09b0be86)

##### <u>Refer below screenshot:</u>

- Functional declarations can be accessed before initialization
- variable declaration if accessed before will return undefined.
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/df43dbb7-7ced-4830-bed9-96aea8d354a8)

##### <u>Reference Error: sing is not defined</u>

- Because it is not hoisted
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/26e8e285-21c4-40af-841e-63b61ba4b418)

##### <u>if var teddy is replaced with let teddy, it will error out</u>

- because let and const are moved to the top
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/eba0f71d-01f5-49aa-aaa2-0500a296e339)

##### <u>functional expressions declared with var</u>

- Function is only going to be run after it was defined
- logging **only sing2 variable** will **result in undefined**.
- e.g. in below invoking the function sing2() **_beforehand will result in TypeError_** not defined
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/84230715-81d8-4a15-80e1-ee0effa11159)

- if you move the function invocation line below, then it will work as per the expectations.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/d370ff0f-33ae-48de-a702-ef5535cfef0e)

##### <u>Below Hoisting Example:</u>

- This returns undefined because of the function execution context
- **_Every time we run a function, `a new execution context gets created` and we have to go through the creation phase and execution phase_**

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/d50d7418-f57c-4c5f-94ff-0c83a07f3d70)

##### <u>Above Code is converted into below code by JS engine by reading the code, that is why we see undefined logged.</u>

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/ea04566d-f3f8-47bf-8396-2de71e0986ac)
