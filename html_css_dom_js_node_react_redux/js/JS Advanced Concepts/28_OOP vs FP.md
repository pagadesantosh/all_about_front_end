### Object Oriented Programming (OOP)

- Organizing the code into units would be called as Object Oriented Programming
- An object is a box containing information and operations that are supposed to refer to the same concept.
- The operations that happen are called as methods.
- Objects are first class citizens
- few operations on common data.
- this, self objects are mutated. (Side effects)
- Imperative
- Quite good if you have many things like characters in a game with not too many operations

---

### Functional Programming (FP)

- Avoiding Side Effects and writing pure functions would be called as Functional Programming
- The code is essentially a combination of functions.
- Data is immutable which leads to writing programs with no side effects and pure functions.
- In a functional Programming paradigm, that function cannot change the outside world and the output value of a function simply depends on the given arguments.
- This allows functional programming to really have control over a program flow.
- Functions are first class citizens
- many operations on fixed data.
- Functions are pure
- Declarative
- Is quite good at processing large data for apps (Ex: analyzing user data for machine learning model)
- Works really well for high performance processors because you can run it on multiple processors
- a few things that require a lot of operations, a lot of little functions apply to it.

---

#### Summary:

In all programs, there are two primary components
- data
- behaviors

***OOP says bring together the data and behavior in a single location called Object or a Class***

***FP says that data and behavior are distinctly different things and should be kept separate for clarity***