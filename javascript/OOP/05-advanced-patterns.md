**Advanced Patterns (Practical Solutions)**

**Composition**
Build complex objects by combining smaller objects.

```js
const canEat = state => ({
  eat: () => `${state.name} eats`
});

const canWalk = state => ({
  walk: () => `${state.name} walks`
});

const createPerson = name => {
  const state = { name };
  return Object.assign({}, canEat(state), canWalk(state));
};

const p = createPerson('Alex');
console.log(p.eat());
console.log(p.walk());
```

**Mixins**
Share behavior across different classes without inheritance.

```js
const LoggerMixin = Base => class extends Base {
  log(msg) {
    return `[${this.label}] ${msg}`;
  }
};

class Service {
  constructor(label) {
    this.label = label;
  }
}

class ApiService extends LoggerMixin(Service) {}

const api = new ApiService('API');
console.log(api.log('ready'));
```

**Factory Functions**
Create objects without `class` or `new`.

```js
function createPoint(x, y) {
  return {
    x,
    y,
    move(dx, dy) {
      this.x += dx;
      this.y += dy;
    }
  };
}

const pt = createPoint(1, 2);
pt.move(2, 3);
console.log(pt);
```
