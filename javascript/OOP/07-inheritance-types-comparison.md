**Inheritance Types: OOP vs JavaScript**

This file compares common inheritance types from a general OOP perspective and how (or if) they map to JavaScript.

**1. Single Inheritance**
A child class inherits from exactly one parent class. This is the only type JavaScript supports directly using the `extends` keyword.

Relationship: `Class B -> Class A`

JS example:
```js
class Dog extends Animal {}
```

**2. Multi-level Inheritance**
A class inherits from a parent, which in turn inherits from another parent. This creates a chain.

Relationship: `Class C -> Class B -> Class A`

JS example:
```js
class Vehicle {}
class Car extends Vehicle {}
class ElectricCar extends Car {}
```

**3. Hierarchical Inheritance**
One parent class has multiple child classes. This is common for sharing a base set of features across different types of objects.

Relationship: `Class B -> Class A` and `Class C -> Class A`

JS example:
```js
class Employee {}
class Developer extends Employee {}
class Designer extends Employee {}
```

**4. Multiple Inheritance**
A child class inherits from more than one parent class simultaneously.

Relationship: `Class C -> Class A` and `Class C -> Class B`

JavaScript status: **Not supported**. JavaScript throws a syntax error if you try to extend two classes. Use mixins to simulate this.

JS (mixin-style) example:
```js
const CanWrite = Base => class extends Base {
  write() { return 'writing'; }
};

const CanDesign = Base => class extends Base {
  design() { return 'designing'; }
};

class Person {}
class Creator extends CanDesign(CanWrite(Person)) {}
```

**5. Hybrid Inheritance**
A combination of two or more of the types above (for example, multi-level + hierarchical). This can lead to the "Diamond Problem" in languages like C++.

JavaScript status: Since JS doesn't support multiple inheritance, it cannot have true hybrid inheritance natively. Use mixins or composition for similar behavior.

---

**Summary Table (Interview Quick View)**

| Inheritance Type | Supported in JS? | How to implement in JS |
| --- | --- | --- |
| Single | Yes | `class Child extends Parent` |
| Multi-level | Yes | `class C extends B` (where `B extends A`) |
| Hierarchical | Yes | Multiple classes extending the same parent |
| Multiple | No | Mixins or composition |
| Hybrid | No | Mixins or composition |
