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
