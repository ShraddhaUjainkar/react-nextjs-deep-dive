**Class Factories in JavaScript**

A class factory is a function that returns a class. This is useful when you need to generate classes dynamically or inject shared behavior.

**Simple Class Factory**

```js
const createModelClass = type => {
  return class {
    constructor(data) {
      this.type = type;
      this.data = data;
    }

    describe() {
      return `${this.type}: ${JSON.stringify(this.data)}`;
    }
  };
};

const UserModel = createModelClass('User');
const OrderModel = createModelClass('Order');

const u = new UserModel({ name: 'Ava' });
const o = new OrderModel({ id: 123 });

console.log(u.describe());
console.log(o.describe());
```

**Factory + Mixins**
Combine with mixins to build specialized class flavors.

```js
const Timestamped = Base => class extends Base {
  constructor(...args) {
    super(...args);
    this.createdAt = new Date();
  }
};

const createEntityClass = (label) => {
  class Entity {
    constructor(id) {
      this.label = label;
      this.id = id;
    }
  }
  return Timestamped(Entity);
};

const Ticket = createEntityClass('Ticket');
const t = new Ticket('T-001');
console.log(t.label, t.id, t.createdAt instanceof Date);
```

**When to use class factories**
- When classes need configuration (e.g., `type`, `schema`, `baseUrl`).
- When you want to generate multiple related classes with the same structure.
