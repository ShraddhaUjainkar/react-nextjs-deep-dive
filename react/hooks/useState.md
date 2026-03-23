# useState Hook

The `useState` hook is used to add **state to functional components**.

Before hooks, state was only available in class components.

---

## Syntax

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>{count}</h2>

      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </div>
  );
}
```

state → current value
setState → function to update value