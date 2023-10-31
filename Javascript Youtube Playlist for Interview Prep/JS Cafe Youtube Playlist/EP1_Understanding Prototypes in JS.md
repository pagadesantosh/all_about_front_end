```js
const myObject = { channelName: "JsCafe" }
console.log(myObject.channelName) // JsCafe
console.log(myObject.hasOwnProperty("channelName")) //true

function myFunction() {
  console.log("Welcome to JsCafe")
}

myFunction.color = "red"
console.log(myFunction()) //
console.log(myFunction.color) //red
console.log(myFunction.toString()) // prints myFunction as it is
console.log(myFunction.hasOwnProperty("color")) //true
```

---

<strong>Global memory</strong>: Space of memory in browser or in JS engine where `javascript stores variables and functions`.

- When Javascript scans the whole code, it stores the objects and functions in the global memory.

```js
//Example for the above code snippet, the global memory looks like below
myObject: {
  channelName: "JsCafe"
}
myFunction: f
```

- Javascript by default adds the property called prototype (for Objects and for Functions) which is again an object (and in this prototype object we have a property named as hasOwnProperty which is a function), some others are like toLocaleString()
- Similarly there are other properties like toLocaleString (which is also a function)
- For every object, Javascript by default adds one more property called `proto`
- Labelled as Object and for this particular function, `proto` points to null

Ex: For myObject by default javascript adds the `proto` property and this points out to the prototype of the Object Function

- So whenever a function is created in javascript it is just not a function but it is a bundle of function and object both.

Ex: myFunction is a function + object which has color property and `proto` (whereas this `proto` property points out to )

![image](https://user-images.githubusercontent.com/42731246/215369453-f30b0815-9ca2-4fe9-b869-6f62706970af.png)

- For the myFunction when we perform hasOwnProperty then the Javascript finds the hasOwnProperty inside the Object (look out the proto mapping)
