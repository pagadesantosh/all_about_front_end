### 1. Javascript Engine:

- There is a **_ECMAScript standard_** which tells that how things work in a specific pattern in Javascript.
- `ECMAScript` is the governing body of `JS` that essentially decides <u>how the language should be standardized</u>.

#### Javascript V8 Engine:

- Written in `C++` programming language
- When we provide the JS files, there will be lexical analysis happening (e.g. refer below screenshot)
  ![alt text](<images used/Javascript Engine.png>)

```diff
- Our JS code is broken into tokens
+ (ex: parser is one of the token we can refer to)
```

- And these tokens are formed into <u>**Abstract Syntax Tree** (AST)</u>. For more details explore website: https://astexplorer.net
- And from `AST`, the code will go through the `Interpreter` and it spits out into `Bytecode` (which is able to be interpreted by Javascript engine)
- **Profiler** is also called as a `monitor` and **watches our code** as it runs and notes on optimizing the code.
- So if the same lines of code are run a few times we pass to the compiler (or JIT Compiler) and this compiler helps us to make optimizations **<u>and then it replaces the sections on where it could be improved of the bytecode with optimized machine</u>**

---

**Note**: There are **two** ways to run Javascript (Interpreter, Compiler)

#### <u>Interpreter:</u>

- `translates` and `read the files` **<u>line by line on the fly</u>**.
- **_<u>Converts the JS code into Bytecode_**</u>.
- Interpreters are usually fast as they don't need to translate into other language
- **The _problem_ with `interpreters`** is **<u>running the same code more than once</u>**, (e.g. loop over 1000 times even though it gives same result), it can get really slow.

#### <u>Complier:</u>

- **<u>doesn't translates code on the fly</u>** whereas it tries to understand what we want to do and **<u>takes our language and changes</u>** it into something else.

- Compiler actually **<u>helps us to overcome the problem of Interpreter mentioned above</u>**,
- It <b style='background:yellow'>takes a little bit more time to start up</b> because it has to go through that compilation (e.g. go through the entire code and spit into another language)
- Compiler is `smart` enough (e.g. when it sees code like this that we just loop over and over), it **<u>can**</u> just **<u>simplify**</u> the code.
- **So, instead of calling multiple times,** just replace this function with the output (output which is rendered after every iteration e.g. 5+4=9)
- **_As the compiler doesn't need to repeat the translation for each pass through in that loop_**, the code generated from it is actually faster. And these sort of things is called optimization

- As we have seen that both have pros and cons, <b><i style='background:yellow'>that is why they came up with combining both Compiler & Interpreter</i></b> and created **JIT Compiler** which is called as **Just In Time Compiler**.
- <u>**_Browsers started using JIT compiler_**</u> to make the engines faster.

$${\color{red}Welcome}$$

<div style="background-color: yellow; ">Text with a background color</div>
