# 🌊 React Hydration Mismatch Guide

### 📍 The Error
> "A tree hydrated but some attributes of the server rendered HTML didn't match the client properties."

### 🔍 What is "Hydration"?
Hydration is the process where React in the browser takes the static HTML sent by the server (SSR) and attaches event listeners to make it interactive. For this to work, the **Server HTML** and the **First Client Render** must be identical.

---

### ⚠️ Common Causes

| Cause | Example |
| :--- | :--- |
| **Dynamic Data** | `Date.now()`, `Math.random()`, or `new Date()`. |
| **Browser Globals** | Using `window`, `document`, or `localStorage` during render. |
| **Locale Mismatch** | Server formats as `MM/DD/YY` while Client uses `DD/MM/YY`. |
| **Invalid HTML** | Placing a `<div>` inside a `<p>` tag (Browser "fixes" this, causing a mismatch). |

---

### 🛠️ Solutions

#### 1. The `isMounted` Hook (Best Practice)
Wait for the component to mount on the client before rendering the dynamic content.

```tsx
"use client";
import { useState, useEffect } from "react";

export default function SafeComponent() {
  const [mounted, setMounted] = useState(false);

  useEffect(() => {
    setMounted(true);
  }, []);

  if (!mounted) return null; // Or a skeleton/placeholder

  return <div>{new Date().toLocaleTimeString()}</div>;
}
```

#### 2. The `suppressHydrationWarning` Prop

```tsx
"use client";

export default function WarningComponent() {
  // This will flash the old value once before correcting itself.
  return (
    <div suppressHydrationWarning>
      {new Date().toLocaleTimeString()}
    </div>
  );
}
```

#### 3. The `key` Trick (For Lists)
If a list item changes its identity (e.g., ID changes), React treats it as a new element, forcing a re-render and fixing hydration.

```tsx
"use client";
import { useState } from "react";

export default function ListComponent() {
  const [items, setItems] = useState([1, 2, 3]);

  return (
    <>
      <button onClick={() => setItems([...items, Date.now()])}>Add Item</button>
      <ul>
        {items.map((id) => (
          // Using Date.now() as key forces a new element on update
          <li key={id}>{new Date().toLocaleTimeString()}</li>
        ))}
      </ul>
    </>
  );
}
```
