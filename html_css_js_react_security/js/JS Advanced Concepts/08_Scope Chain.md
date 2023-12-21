### 8. Scope Chain:

- Each context has a link to its outside world or a link to his parent and the outer environment depends on where the function sits.
- **_Lexical means where the function is written_**

##### <u>Below Example:</u>

- All of these functions has access to the global scope (**_in our case it is var x='x'_** which is declared on the global scope)

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/a9e6b323-897a-4259-9e71-b496826a49f0)

- eval and width are not a good idea to optimize our code because you can change how scope works internally with these two things which makes difficult.

- any variable that is declared inside the function, it will be accessed inside any function scope which are defined inside.

- any variable that is declared inside the curly brackets with let and const can be accessed only in the block scope, whereas in this case var acts like a function scope

- if var is replaced with let, then it acts as a block scope and we will get reference error.
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/ce356867-f37c-4e19-8ef1-be1d8edd9804)
