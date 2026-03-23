
## Overview
useCallback caches the function definition itself so the memory address stays the same, preventing child components from re-rendering unnecessarily.

## Basic Syntax
```javascript
const cachedFn = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```

## When to Use It
 - Preventing Child Re-renders: When you pass a function to a child component wrapped in React.memo. Without useCallback, the child sees a "new" function every time and re-renders.

 - Throttling/Debouncing: When you want to ensure a debounced function persists across renders instead of being reset.

## Difference from useMemo
useMemo runs the function and returns the Result.

useCallback returns the Function itself without running it.