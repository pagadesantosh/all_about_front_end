### We need at least +, -, x, %,

```js
function Calculator() {
  let value = 0;

  return {
    add: function (number) {
      value += number;
      return this;
    },
    multiply: function (number) {
      value *= number;
      return this;
    },
    subtract: function (number) {
      value -= number;
      return this;
    },
    modulus: function (number) {
      if (number !== 0) {
        value %= number;
      }
      return this;
    },
    result: function () {
      return value;
    },
  };
}

// Usage
const calc = Calculator();
const res = calc.add(10).multiply(5).subtract(30).add(10).modulus(7).result();
console.log(res); // 2, because that is the remainder
```
