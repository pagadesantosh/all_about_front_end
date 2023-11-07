###1. When JS is after the body tag

```js
<html>
  <head>Title</head>
  <body></body>
  <script src='script.js'></script>
</html>
```

**Ex**: Once HTML parsing is done, it encounters the JS, it downloads the JS and then it executes the JS.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/8cf65d6b-c906-4291-b640-761a2872b760)

---

### 2. When JS is in HEAD tag

```js
<html>
  <head>
    <title>Title</title>
    <script src='script.js'></script>
  </head>
  <body></body>
</html>
```

**Ex**: During HTML parsing it encounters the JS and it pauses the HTML parsing and it downloads the JS and then it executes the JS and then HTML parsing is resumed.

**Cons**: It stops the execution of DOM tree which is a bad User experience.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/d5066c05-458c-4da9-8674-af0627a277ea)

---

### 3. When async attribute is in HEAD tag

```js
<html>
  <head>
    <title>Title</title>
    <script async src='script.js'></script>
  </head>
  <body></body>
</html>
```

**Ex**:

- During HTML parsing it encounters the JS and the HTML parsing is continued during download phase

- But when it executes the JS, the HTML parsing is paused and once it executes the JS then HTML parsing is resumed.

**Cons**: It stops the execution of DOM tree which is a bad User experience.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/28920fe6-cada-49e5-a2de-21e7a8922515)

---

### 4. When defer attribute is in HEAD tag

```js
<html>
  <head>
    <title>Title</title>
    <script defer src='script.js'></script>
  </head>
  <body></body>
</html>
```

**Ex**:

- During HTML parsing it encounters the JS and the HTML parsing is continued during download phase

- After HTML parsing is completed, it executes the JS.

**Note**: This is more optimized approach when compared to others because we are prefetch the Javascript code during the parsing phase.

![image](https://github.com/saiteja-gatadi1996/interview_prep/assets/42731246/d24eb584-0bf9-43e6-a84a-8fc68e8bf04b)

---
