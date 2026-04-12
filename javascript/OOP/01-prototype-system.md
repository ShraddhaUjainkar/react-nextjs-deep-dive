**The Prototype System**

**The Prototype Chain**
Property lookup in JavaScript walks the object's internal `[[Prototype]]` chain. If a property isn't found on the object itself, the engine looks at its prototype, then that prototype’s prototype, until it reaches `null`.

```js
const animal = { eats: true };
const dog = Object.create(animal);
dog.barks = true;

console.log(dog.barks); // true (own property)
console.log(dog.eats);  // true (found on prototype)
console.log(Object.getPrototypeOf(dog) === animal); // true
```

**Prototypal Inheritance**
Objects can inherit directly from other objects without classes.

```js
const vehicle = {
  move() {
    return 'moving';
  }
};

const car = Object.create(vehicle);
car.drive = function () {
  return 'driving';
};

console.log(car.move());  // "moving"
console.log(car.drive()); // "driving"
```

**Constructor Functions (Pre-ES6)**
Functions can be used as constructors with `new`. Methods are placed on `FunctionName.prototype` so all instances share them.

```js
function Person(name) {
  this.name = name;
}

Person.prototype.sayHi = function () {
  return `Hi, I'm ${this.name}`;
};

const ada = new Person('Ada');
console.log(ada.sayHi());
```

**`__proto__` vs `prototype`**
`__proto__` (or `Object.getPrototypeOf`) is the *actual link* from an instance to its prototype. `prototype` is a property on constructor functions used when creating instances with `new`.

```js
function User(name) { this.name = name; }
const u = new User('Sam');

console.log(u.__proto__ === User.prototype); // true
console.log(User.prototype.constructor === User); // true
```
