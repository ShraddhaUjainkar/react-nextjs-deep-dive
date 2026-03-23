# React Hooks: useEffect vs. useLayoutEffect

This guide covers the technical differences, use cases, and performance implications of React's primary side-effect hooks.

---

## 1. Quick Comparison Table

| Feature            | `useEffect`                         | `useLayoutEffect`                   |
| :----------------- | :---------------------------------- | :---------------------------------- |
| **Execution** | **Asynchronous** (After paint)      | **Synchronous** (Before paint)      |
| **Browser Paint** | Screen updates *before* it runs     | Screen updates *after* it runs      |
| **Performance** | Better (Non-blocking)               | Potential lag (Blocking)            |
| **Primary Goal** | Data fetching, logging, events      | Measuring DOM, fixing UI "jumps"    |

---
## 2. The Rendering Lifecycle

Understanding the "Critical Rendering Path" is key to knowing which hook to use. 

1. **React Render**: React calculates what the DOM should look like.
2. **DOM Mutation**: React changes the actual DOM nodes.
3. **`useLayoutEffect`**: Runs here. It can read the DOM and make further changes.
4. **Browser Paint**: The browser draws the changes to the screen.
5. **`useEffect`**: Runs here. The user has already seen the update.



---

## 3. Real-World Scenario: Tooltip Positioning

Imagine a tooltip that needs to be centered above a button.

### Problem with `useEffect`:
1. The tooltip renders at a default position (e.g., `top: 0`).
2. The browser **paints** the tooltip at `top: 0`.
3. `useEffect` runs, measures the button, and calculates the correct position.
4. The browser **paints again**.
5. **Result:** The user sees a "flicker" as the tooltip jumps from the top to the button.

### Solution with `useLayoutEffect`:
1. The tooltip renders at default.
2. `useLayoutEffect` runs **immediately**, measures the button, and updates the position.
3. The browser **paints once** with the tooltip in the correct spot.
4. **Result:** A perfectly smooth UI with no flicker.



---
## 4. Next.js & SSR (Server-Side Rendering)

In Next.js, components are rendered on the server where there is no browser "layout." Using `useLayoutEffect` directly will trigger a console warning.

### The "Isomorphic" Fix
Professional libraries use this pattern to avoid SSR warnings:

```javascript
import { useEffect, useLayoutEffect } from 'react';

// Check if we are in the browser (client-side)
const useIsomorphicLayoutEffect = 
  typeof window !== 'undefined' ? useLayoutEffect : useEffect;

export default function MyComponent() {
  useIsomorphicLayoutEffect(() => {
    // This is safe for Next.js
    console.log("Running layout logic on the client!");
  }, []);

  return <div>Next.js Ready Component</div>;
}
```

## 5. Final Summary: When to Use What?
Use `useEffect` (99% of the time): For API calls, setting up subscriptions, or changing state that doesn't immediately affect how an element is positioned.

Use `useLayoutEffect` (1% of the time): Only when you need to measure a DOM element's size/position or if you notice a visual "glitch" during a state update.