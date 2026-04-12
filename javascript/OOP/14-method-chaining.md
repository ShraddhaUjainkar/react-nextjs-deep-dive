**Method Chaining in JavaScript**

Method chaining lets you call multiple methods in a single statement by returning `this` (or another object) from each method.

**Basic Example**

```js
class Calculator {
  constructor(value = 0) {
    this.value = value;
  }

  add(n) {
    this.value += n;
    return this;
  }

  subtract(n) {
    this.value -= n;
    return this;
  }

  multiply(n) {
    this.value *= n;
    return this;
  }

  result() {
    return this.value;
  }
}

const calc = new Calculator(10);
const answer = calc.add(5).subtract(2).multiply(3).result();
console.log(answer); // 39
```

**Chaining with Objects**

```js
const builder = {
  value: 0,
  add(n) { this.value += n; return this; },
  reset() { this.value = 0; return this; }
};

console.log(builder.add(2).add(3).reset().value); // 0
```

**Key Rule**
- Return `this` from each method you want to chain.
