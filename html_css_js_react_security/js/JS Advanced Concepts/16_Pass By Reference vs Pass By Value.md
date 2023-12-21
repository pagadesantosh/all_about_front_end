### 16. Pass By Reference vs Pass By Value

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
let deepClone = JSON.stringify(JSON.parse(originalObj));
```