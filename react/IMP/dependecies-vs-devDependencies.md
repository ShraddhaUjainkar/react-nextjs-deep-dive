# 📦 `dependencies` vs `devDependencies`

## The Simple Idea
> Think of it this way: **dependencies** are what your *users* need. **devDependencies** are what *you* need while building.

---

## Comparison Table

| Feature | `dependencies` | `devDependencies` |
| :--- | :--- | :--- |
| **What it is** | Tools your app needs to **run**. | Tools you need to **build** the app. |
| **In Production?** | ✅ Included in the final bundle. | ❌ Excluded from the final bundle. |
| **Purpose** | Running the app. | Building, testing, and styling. |
| **Command** | `npm install <name>` | `npm install <name> -D` |
| **Size Impact** | Makes your final website larger. | Does not affect website load speed. |

---

## 🧠 Key Concepts (Simple Language)

### 1. What goes in `dependencies`?
Packages your app **cannot work without** in production.
- `react`, `react-dom` — your UI framework
- `next` — the server/routing engine
- `axios` — for making API calls at runtime

### 2. What goes in `devDependencies`?
Packages only needed **during development or build time** — they are never shipped to the user.
- `typescript` — type checking (done before build, not at runtime)
- `eslint`, `prettier` — code quality tools
- `jest`, `vitest` — testing frameworks
- `tailwindcss` — generates CSS during build, not needed after

### 3. Why does it matter?
When you deploy to a server and run `npm install --production`, npm **skips devDependencies**. This keeps your production `node_modules` smaller and your deployments faster.

### 4. The `-D` flag
```bash
npm install typescript -D
# same as
npm install typescript --save-dev
```
This automatically puts the package in `devDependencies` in your `package.json`.

### 5. Common Mistake ⚠️
Putting a dev tool (like `eslint`) in `dependencies` by accident (forgetting `-D`). It won't break anything, but it **bloats your production bundle** unnecessarily.