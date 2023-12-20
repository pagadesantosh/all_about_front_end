### 1. Javascript Engine:

- There is a **ECMAScript standard** which tells that how things work in a specific pattern in Javascript.
- ECMAScript is the governing body of JS that essentially decides how the language should be standardized.

#### Javascript V8 Engine:

- Written in C++ programming language
- When we provide the JS files, there will be lexical analysis happening (e.g. refer below screenshot)
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/60e29b0e-9054-42a5-ab65-41eb55d7cfd2)
- Our JS code is broken into tokens (ex: parser is one of the token we can refer to)
- And these tokens are formed into **Abstract Syntax Tree** (AST). For more details explore website: https://astexplorer.net
- And from AST, the code will go through the Interpreter and it spits out into Bytecode (which is able to be interpreted by Javascript engine)
- **Profiler** is also called as a monitor and **watches our code** as it runs and notes on optimizing the code. So if the same lines of code are run a few times we pass some of this code to the compiler (or JIT Compiler) and this compiler helps us to make optimizations **and then it replaces the sections on where it could be improved of the bytecode with optimized machine**

---

**Note**: There are two ways to run Javascript (Interpreter, Compiler)

#### <u>Interpreter:</u>

- translates and read the files line by line on the fly. Converts the JS code into Bytecode.
- Interpreters are usually fast as they don't need to translate into other language
- **The problem with interpreters** is running the same code more than once, (e.g. loop over 1000 times even though it gives same result), it can get really slow.

#### <u>Complier:</u>

- doesn't translates code on the fly whereas it tries to understand what we want to do and takes our language and changes it into something else

- **Compiler actually helps us** to overcome the problem of Interpreter mentioned above,
- It takes a little bit more time to start up because it has to go through that compilation (e.g. go through the entire code and spit into another language)
- Compiler is smart enough (e.g. when it sees code like this that we just loop over and over), it can just simplify the code.
- **So, instead of calling multiple times,** just replace this function with the output (output which is rendered after every iteration e.g. 5+4=9)
- As the compiler doesn't need to repeat the translation for each pass through in that loop, the code generated from it is actually faster. And these sort of things is called optimization

- As we have seen that both have pros and cons, that is why they came up with combining both Compiler & Interpreter and created **JIT Compiler** which is called as **Just In Time Compiler**.
- Browsers started using JIT compiler to make the engines faster

---

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

---

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

---

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

---

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

---

### 6. Lexical Environment

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/22a89184-0581-4c03-8a52-291e85dfb1c4)

- This function `a` is lexically inside findName function

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/6a3ff6ce-73b2-4102-b5fb-09a72f416fcd)

- So execution context is going to tell you which lexical environment is currently running.

---

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

---

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

---

### 9. Global Variables:

- Too many Global variables, pollutes the Global Execution Context
- Which Eventually leads to memory leaks and making things slower and slower until our browsers crash.
- The issue with Global Variables is that we can have variable collisions.

##### <u>Refer Screenshot:</u>

- **_This is because everything is on Global Execution context and they overwrite each other if there's any duplicates_**
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/8b8dae44-456d-4536-9b8e-c4e2eb29f10f)
- So this creates a lot of possible bugs

---

### 10. IIFE's:

- Using this Immediately Invoked Function Expression, we can place all the code inside of local scope to avoid any namespace collisions.
- When JS Engine comes across this brackets, it automatically makes it into a function expression (not functional declaration)
- IIFE can be a named function also, but generally in most of the cases we use it as anonymous functions and invoke them immediately.

##### <u>:Refer Example Screenshot</u>

- Below is not the same case for functional declarations
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/c613dfda-387f-451c-b11f-c6a94c362ef4)

---

### this keyword:

- this is the object that the function is a property of

##### <u>Example 1:</u>

```js
function a() {
  console.log(this); // Window
}
a();
```

##### <u>Example 2:</u>

```js
function b() {
  'use strict';
  console.log(this); // undefined
}
b();
```

- **_Inside a object, if there is any function property_**, then this keyword refers to its object.
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/a031dd50-a015-48ce-ba5e-7e1a2aae010d)

- anotherFunc is invoked inside sing() method property, and when we log `this` it logs **_Window object_**

- this keyword is **_dynamically scoped_**. It doesn't matter where it's written, **_it matters on how the function is called_**.

##### <u>Arrow functions solve the problem here:</u>

- Arrow functions has a lexical this behavior unlike normal functions (so it lexically bind this)
- In our below case (whatever the object is surrounding this while the main object is)
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/fe8d6530-cf3c-4886-934d-9d730037e391)

##### <u>Before ES6, by applying `bind`:</u>

- **_return the anotherFunc and bind to this_**
- as we are returning this piece of code outside the functional expression code, `this keyword mentioned in the bind` refers to the object

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/51d08d7b-e88e-4cff-95e6-68fe76da2b89)

##### <u>Before ES6, using reference variable:</u>

- outside to the function expression itself, we will create a reference
- e.g. `var self = this;`
- At the time the above code is ran, **_self start maintaining that reference to the object_** so that **we can use self** going forward **_(instead of this)_**

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/b2794857-a535-4325-bd04-592657a3a5ee)

---

### 11. Call Apply Bind:

- In order to manipulate `this` keyword, there are three important methods.
- In order to borrow methods, we can make use of call apply bind.

**Call**: underneath the hood, all functions when created have this property called call that allows us to call/invoke the function

```js
// call syntax:
Function.call(context, thisArg, thisArg1, thisArg2);
```

**apply**: instead of a.call(), we can also use a.apply() in one of this case.

```js
// apply syntax:
Function.apply(context, [thisArg1, thisArg2, thisArg3]);
```

```js
// bind syntax:
const newFunc = Function.bind(context, thisArg1, thisArg2, thisArg3);
```

```js
function a() {
  console.log('hi'); // hi
}

a.call();
```

```js
// object 1 has heal method
const wizard = {
  name: 'Merlin',
  health: 100,
  heal() {
    return (this.health = 100);
  },
};

wizard.heal(); // 100

// object 2 is in need of heal method
const archer = {
  name: 'Robin Hood',
  health: 30,
};

// So, in order to borrow heal method from wizard object, we use `call, apply, bind`

// instead of using wizard to call heal, it uses archer to call heal
console.log('1', archer); // logs the original archer object with health 30
wizard.heal.call(archer);
console.log('2', archer); // logs the mutated archer object with health 100
```

---

```js
// object 1 has heal method
const wizard = {
  name: 'Merlin',
  health: 100,
  heal(num1, num2) {
    return (this.health += num1 + num2);
  },
};

wizard.heal(); // 100

// object 2 is in need of heal method
const archer = {
  name: 'Robin Hood',
  health: 30,
};

// So, in order to borrow heal method from wizard object, we use `call, apply, bind`

// instead of using wizard to call heal, it uses archer to call heal
console.log('1', archer); // logs the original archer object with health 30
wizard.heal.call(archer, 50, 30);
// wizard.heal.apply(archer, [50, 30]);
// const healArcher = wizard.bind(archer, 50, 30)
// healArcher()
console.log('2', archer); // logs the mutated archer object with health 100
```

---

### 12. bind and currying

- we can reuse the function and pass any second parameter (Ex: 4 in the first case, 10 in the second case)
  ![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/04c6a89b-2fab-4cfa-8c66-4c3cecd67491)

---

#### Examples

- b.say() logs the `b` object
- c.say() if double invoked logs the `Window` object
- d.say() if double invoked logs the {name: 'jay', say:[Function]}

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/1a87f82a-e8de-4047-bbf6-474c5147eefc)

---

### 13. Context vs Scope

**Scope**

- Scope is a **_function_** based
- Scope means what is the variable axis of a function when it is invoked and what is in the variable environment.

**Context**

- Context, on the other hand, is more about object based.
- Context says **_what's the value of the this keyword_**, which is a reference to the object that owns that current executing code.

**_Context is most often determined by how a function is invoked with the value of this keyword and scope
refers to the visibility of variables._**

---

### 14. Javascript Data Types

**_There are 7 JS data types_**

```js
/* Primitives: types other than object type are all primitives (It is a data that only represents a single value)*/
- Number
- String
- Boolean
- undefined (absence of a definition for a variable)
- null (absence of value + intentionally provided value )

/* Non-primitives: Doesn't contain the actual value directly, whereas it has reference similar to a pointer to somewhere in memory that the object is held */
- Object
- Symbol (usually used for object properties so that their property is **_unique_**)
```

<b><u>Note:</u></b> typeof function(){} returns function but underneath the hood, **_functions are just objects_**

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/6331d4f9-f8c3-4cb5-b2b8-1fe741e09de2)

<b><u>Note:</u></b> Primitives are immutable (in order to change them, remove the primitive type and assign with a new value )

---

### 15. Pass By Reference vs Pass By Value

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/be0de22b-710b-4b73-b50d-115bf2b01c2a)

**Pass By Value**: Primitives follow this pass by value, which are only changed when a new value is assigned to them in memory.

e.g. If we have variables a & b (then they really don't know each other)
![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/16351786-5839-4b84-82cd-06c14e114161)

**_Summary:_** Pass by value simply means we copy the value and we create that value somewhere else in memory.

**Pass By Reference**: Objects follow this pass by reference.

- If you assign one of the object to another and If you change the reference of one object, then the other object also updates

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/cce8253d-3723-4207-89ea-7b509abcc62f)

```js
//output:
{name: 'Yao', password: 'easypeasy',}
{name: 'Yao', password: 'easypeasy'}

```

<u>**Solutions**:</u>
**_Solution 1_**: `let clonedObj = Object.assign({}, originalObj)`
**_Solution 2_**: `let clonedObj = {...originalObj}`

<u>**Limitations of Object.assign and spread**:</u>

- This doesn't work for nested objects
- Because it **_does the shallow clone_**, which means it only clones first layer

```js
let obj = {
  a: 'a',
  b: 'b',
  c: { deep: 'try and copy' },
};

let clone1 = Object.assign({}, obj);
let clone2 = { ...obj };

obj.c.deep = 'hahaha';
console.log(obj); // {a: 'a', b: 'b', c: { deep: 'hahaha' }}
console.log(clone1); // {a: 'a', b: 'b', c: { deep: 'hahaha' }}
console.log(clone2); // {a: 'a', b: 'b', c: { deep: 'hahaha' }}
```

<u>**Solution for Deep Clone instead of shallow clone**:</u>
```js
let deepClone = JSON.stringify(JSON.parse(originalObj))
```
