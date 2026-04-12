**Interview Problem-Solving Topics**

**The `this` Keyword**
In classes, instance methods use dynamic `this` based on the call site. Arrow functions capture `this` from the surrounding scope.

```js
class Button {
  constructor() {
    this.label = "Click";
  }

  handle() {
    return this.label;
  }

  handleArrow = () => {
    return this.label;
  };
}

const b = new Button();
const h1 = b.handle;
const h2 = b.handleArrow;

// h1() would be undefined in strict mode because `this` is lost
console.log(h2()); // "Click"
```

**Memory Efficiency**
Methods on the prototype are shared across instances, saving memory.

```js
function Item(name) {
  this.name = name;
}

Item.prototype.describe = function () {
  return `Item: ${this.name}`;
};

const a = new Item("A");
const b = new Item("B");
console.log(a.describe());
console.log(b.describe());
```

**The Diamond Problem**
In classic multiple inheritance, two parents might define the same method, creating ambiguity. JavaScript avoids this by only allowing single inheritance. We simulate reuse with composition or mixins.

```js
const CanFly = (Base) =>
  class extends Base {
    fly() {
      return "flying";
    }
  };

const CanSwim = (Base) =>
  class extends Base {
    swim() {
      return "swimming";
    }
  };

class Animal {}
class Duck extends CanSwim(CanFly(Animal)) {}

const d = new Duck();
console.log(d.fly());
console.log(d.swim());
```

## "Does JavaScript support multiple inheritance?", the correct answer is:

"No, JavaScript has a single-parent prototype chain. However, we can achieve the same result using Mixins or Object.assign() to copy properties from multiple sources into a single class."
