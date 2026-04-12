**Encapsulation and Data Privacy**

**Private Fields (`#`)**
True private fields are only accessible inside the class body.

```js
class Counter {
  #count = 0;

  increment() {
    this.#count += 1;
    return this.#count;
  }
}

const c = new Counter();
console.log(c.increment());
// c.#count; // SyntaxError
```

**Getters and Setters (`get` / `set`)**
Control how properties are read and written.

```js
class Temperature {
  constructor(celsius) {
    this._celsius = celsius;
  }

  get fahrenheit() {
    return this._celsius * 1.8 + 32;
  }

  set fahrenheit(f) {
    this._celsius = (f - 32) / 1.8;
  }
}

const t = new Temperature(0);
console.log(t.fahrenheit); // 32
```

**Closure-based Privacy**
Before private fields, closures were used to hide data.

```js
function createBankAccount() {
  let balance = 0;

  return {
    deposit(amount) {
      balance += amount;
      return balance;
    },
    getBalance() {
      return balance;
    }
  };
}

const account = createBankAccount();
console.log(account.deposit(50));
console.log(account.getBalance());
```
