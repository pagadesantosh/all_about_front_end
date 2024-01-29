### 9. Global Variables:

- Too many Global variables, pollutes the Global Execution Context
- Which Eventually leads to memory leaks and making things slower and slower until our browsers crash.
- The issue with Global Variables is that we can have variable collisions.

##### <u>Refer Screenshot:</u>

- **_This is because everything is on Global Execution context and they overwrite each other if there's any duplicates_**
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/8b8dae44-456d-4536-9b8e-c4e2eb29f10f)
- So this creates a lot of possible bugs
