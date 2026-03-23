
## Overview

useMemo caches the result of a calculation (like an object or a filtered list) so you don't have to re-compute or re-create it on every render.
Basic Syntax

```javascript
const cachedValue = useMemo(() => {
  return calculateResult(a, b);
}, [a, b]);
```

## When to Use It
Skipping Expensive Calculations: If you have a function that filters 5,000 rows of data, use useMemo so it only runs when the search query changes.

Stable Object References: To prevent a child component from re-rendering due to Shallow Comparison when you pass an object as a prop.

##  The Dependency Array
[]: The value is calculated once and never changes.

[data]: The value is recalculated only when data changes.