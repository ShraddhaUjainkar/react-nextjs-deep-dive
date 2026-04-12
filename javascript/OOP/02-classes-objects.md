**Classes and Objects**

**Class Declaration**
Modern syntax for defining constructor functions and prototype methods.

```js
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  area() {
    return this.width * this.height;
  }
}
```

**Object Instantiation**
Instances are created with `new`.

```js
const r = new Rectangle(5, 3);
console.log(r.area()); // 15
```

**The `constructor` Method**
Runs automatically during `new` to initialize instance-specific data.

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const u = new User('Lee');
```

**Instance Methods vs. Static Methods**
Instance methods act on individual objects. Static methods live on the class itself and are called as `ClassName.method()`.

```js
class MathUtil {
  constructor(value) {
    this.value = value;
  }

  double() {
    return this.value * 2;
  }

  static add(a, b) {
    return a + b;
  }
}

const m = new MathUtil(4);
console.log(m.double()); // 8
console.log(MathUtil.add(2, 3)); // 5
```
