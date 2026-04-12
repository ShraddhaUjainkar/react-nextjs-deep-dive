**SOLID Principles (OOP + JavaScript)**

SOLID is a set of design principles that help build maintainable, scalable code.

**S — Single Responsibility Principle (SRP)**
A class or module should have only one reason to change.

```js
// Bad: One class does too much
class Report {
  generate(data) { /* ... */ }
  saveToFile(path) { /* ... */ }
}

// Better: Split responsibilities
class ReportGenerator {
  generate(data) { /* ... */ }
}

class ReportStorage {
  saveToFile(path, report) { /* ... */ }
}
```

**O — Open/Closed Principle (OCP)**
Code should be open for extension but closed for modification.

```js
class Discount {
  apply(price) { return price; }
}

class StudentDiscount extends Discount {
  apply(price) { return price * 0.9; }
}

function finalPrice(price, discount) {
  return discount.apply(price);
}
```

**L — Liskov Substitution Principle (LSP)**
Subtypes must be substitutable for their base types without breaking behavior.

```js
class Bird {
  fly() { return 'flying'; }
}

class Sparrow extends Bird {}

// Avoid: Penguin that breaks expected behavior
class Penguin extends Bird {
  fly() { throw new Error('Cannot fly'); }
}
```

**I — Interface Segregation Principle (ISP)**
Clients shouldn’t be forced to depend on methods they don’t use.

```js
// Prefer small, focused interfaces (or classes in JS)
class Printer {
  print() { /* ... */ }
}

class Scanner {
  scan() { /* ... */ }
}
```

**D — Dependency Inversion Principle (DIP)**
Depend on abstractions, not concrete implementations.

```js
class StripeGateway {
  charge(amount) { return `charged ${amount}`; }
}

class PaymentService {
  constructor(gateway) {
    this.gateway = gateway; // abstraction via injected dependency
  }
  pay(amount) {
    return this.gateway.charge(amount);
  }
}

const service = new PaymentService(new StripeGateway());
console.log(service.pay(50));
```
