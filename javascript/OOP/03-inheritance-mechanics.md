**Inheritance Mechanics**

**The `extends` Keyword**
Creates a child class that inherits from a parent class.

```js
class Animal {
  speak() {
    return 'sound';
  }
}

class Dog extends Animal {
  bark() {
    return 'woof';
  }
}

const d = new Dog();
console.log(d.speak());
console.log(d.bark());
```

**The `super()` Keyword**
Calls the parent constructor and allows access to parent methods.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hi ${this.name}`;
  }
}

class Student extends Person {
  constructor(name, major) {
    super(name);
    this.major = major;
  }
}

const s = new Student('Maya', 'CS');
console.log(s.greet());
```

**Method Overriding (Polymorphism)**
A child can redefine a parent method.

```js
class Bird {
  fly() {
    return 'flying';
  }
}

class Penguin extends Bird {
  fly() {
    return 'cannot fly';
  }
}

console.log(new Penguin().fly());
```

**Single Inheritance Constraint**
JavaScript classes can only extend one parent. Multiple inheritance is avoided to prevent conflicts. Composition and mixins are used instead.
