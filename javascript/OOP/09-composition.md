**Composition in JavaScript**

Composition means building complex objects by combining small, focused behaviors. Instead of saying "is-a" (inheritance), composition is "has-a".

**Why composition?**
- More flexible than inheritance.
- Easier to test and reuse.
- Avoids fragile base class problems.

**Composable Behavior Functions**

```js
const canEat = state => ({
  eat: () => `${state.name} eats`
});

const canSleep = state => ({
  sleep: () => `${state.name} sleeps`
});

const canWork = state => ({
  work: () => `${state.name} works`
});

const createPerson = name => {
  const state = { name };
  return Object.assign({}, canEat(state), canSleep(state), canWork(state));
};

const person = createPerson('Alex');
console.log(person.eat());
console.log(person.sleep());
console.log(person.work());
```

**Composition vs Inheritance (quick check)**
- If behavior changes often or is optional, use composition.
- If a strict "is-a" relationship is stable, inheritance is okay.
