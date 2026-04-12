**Memory Efficiency in JavaScript OOP**

To reduce memory usage, avoid creating duplicate methods per instance.

**Prototype Methods vs Instance Methods**

```js
// Memory-heavy: each instance gets its own copy
function Item(name) {
  this.name = name;
  this.describe = function () {
    return `Item: ${this.name}`;
  };
}

// Memory-efficient: shared method on prototype
function BetterItem(name) {
  this.name = name;
}

BetterItem.prototype.describe = function () {
  return `Item: ${this.name}`;
};
```

**Classes (same idea under the hood)**

```js
class Product {
  constructor(name) {
    this.name = name;
  }
  info() {
    return `Product: ${this.name}`;
  }
}
```

**When instance methods are okay**
- If the method needs to close over constructor-local variables.
- If each instance needs a different version of the method.
