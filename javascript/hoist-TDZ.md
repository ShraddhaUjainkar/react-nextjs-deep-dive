# Hoisting vs TDZ

## Hoisting

Hoisting means JavaScript **moves variable declarations to the top of the scope before execution**.

Example:

```js
console.log(a);
var a = 5;
```

JavaScript treats it like:

```js
var a;
console.log(a);
a = 5;
```

Output:

```
undefined
```

---

## TDZ (Temporal Dead Zone)

TDZ is the **time between hoisting and variable initialization** for `let` and `const`.

Example:

```js
console.log(a);
let a = 5;
```

Output:

```
ReferenceError
```

Because `let` and `const` are **hoisted but not initialized immediately**.

---

## Quick Difference

| Feature       | var      | let         | const       |
| ------------- | -------- | ----------- | ----------- |
| Scope         | Function | Block       | Block       |
| Hoisting      | Yes      | Yes (TDZ)   | Yes (TDZ)   |
| Redeclaration | Allowed  | Not allowed | Not allowed |
| Reassignment  | Allowed  | Allowed     | Not allowed |

---

## Best Practice

* Use **const** by default
* Use **let** if value changes
* Avoid **var**
