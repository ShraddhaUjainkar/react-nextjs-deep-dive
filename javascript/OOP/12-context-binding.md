**Context Binding (`this`) in JavaScript**

Context binding defines what `this` refers to inside a function.

**Default Binding**
In strict mode, `this` is `undefined` for plain function calls.

```js
'use strict';
function show() { return this; }
console.log(show()); // undefined
```

**Implicit Binding**
When a function is called as a method, `this` is the object before the dot.

```js
const user = {
  name: 'Riya',
  greet() { return `Hi ${this.name}`; }
};

console.log(user.greet());
```

**Explicit Binding**
Use `call`, `apply`, or `bind` to control `this`.

```js
function greet() { return `Hi ${this.name}`; }
const person = { name: 'Sam' };

console.log(greet.call(person));
```

**Arrow Functions**
Arrow functions capture `this` from the surrounding lexical scope.

```js
function Counter() {
  this.count = 0;
  setInterval(() => {
    this.count += 1;
  }, 1000);
}
```

**Class Methods and `this`**
Methods are not auto-bound in JS classes. You can bind in the constructor or use class fields with arrow functions.

```js
class Button {
  constructor(label) {
    this.label = label;
    this.handle = this.handle.bind(this);
  }
  handle() { return this.label; }

  handleArrow = () => this.label;
}
```
