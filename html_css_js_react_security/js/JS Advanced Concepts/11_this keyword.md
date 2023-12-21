### 11. this keyword:

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
