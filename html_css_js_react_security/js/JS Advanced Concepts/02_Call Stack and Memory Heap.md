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

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/8db3500f-8762-4d74-86ec-e371b5867bf8)

##### <u>Example Scenario:</u>

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/8e72e16c-3f7c-4265-ba9a-2fa03bd0015c)

##### <u>Below shows us how Call Stack work behind the scenes:</u>

<i>Below is the code:</i>
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/c5e5034b-249c-4aef-948e-ba26fff499b2)

**Global Execution Context**: (anonymous)
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/ab80b134-4c80-4562-a2d9-5c2d401836ad)

**After calculate() function is invoked**, it is added to the top of the Call Stack

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/fc43baa4-ab46-4b14-9aa6-86edc20c0510)

**After subtractTwo() function is invoked**, it is added to the top of the call stack
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/2f21a256-3a29-41cb-8860-5415c40f3858)

**Note:** We can get Maximum call stack size exceeded in one of the scenarios like **Recursion** which means a function calling itself
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/2ff8f8d9-0473-4831-9b7f-ab6cd6cd0dd8)
