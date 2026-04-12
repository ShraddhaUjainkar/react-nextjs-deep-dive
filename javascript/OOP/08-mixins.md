**Mixins in JavaScript**

Mixins are reusable chunks of behavior that can be composed into classes or objects without using classical inheritance. They help you share functionality across unrelated types.

**Why use mixins?**
- Avoid deep inheritance trees.
- Share behavior across multiple classes.
- Keep classes small and focused.

**Functional Mixin Pattern (most common)**

```js
const CanLog = Base => class extends Base {
  log(message) {
    return `[${this.label}] ${message}`;
  }
};

const CanSave = Base => class extends Base {
  save() {
    return `${this.label} saved`;
  }
};

class Service {
  constructor(label) {
    this.label = label;
  }
}

class ApiService extends CanSave(CanLog(Service)) {}

const api = new ApiService('API');
console.log(api.log('ready'));
console.log(api.save());
```

**Object Mixin Pattern**
Useful for plain objects (no classes).

```js
const canWalk = {
  walk() {
    return `${this.name} walks`;
  }
};

const canTalk = {
  talk() {
    return `${this.name} talks`;
  }
};

const person = Object.assign({ name: 'Sam' }, canWalk, canTalk);
console.log(person.walk());
console.log(person.talk());
```

**Notes**
- Mixins can cause method name collisions. Decide which mixin should "win" if names overlap.
- For data privacy, prefer closures or private fields in the base class.
