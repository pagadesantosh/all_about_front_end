### 4. Memory Leaks:

- Memory leaks **_are pieces of memory that the application have used_** `in the past`, _but is not needed any longer_ <u>but has not yet been returned back to us to the pool of free memory</u>.

##### <u>Example:</u>

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/3f8d3097-4b66-419d-abd6-88b7f8582bd0)

##### <u> 3 common Memory leaks:</u>

1. Global Variables

- If these are deeply nested objects, then it will use memory more. So try to avoid declaring more Global variables.

2. Event Listeners

- Adding event listeners and forget to remove them

3. Timers

- clear the timers