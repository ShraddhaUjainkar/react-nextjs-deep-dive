# `useTransition` (React)

`useTransition` lets you update the state without blocking the UI. It marks a state update as a "transition", telling React that it is less urgent than other interactions like typing or clicking, and should be interruptible.

## 📌 Key Rules
- **Import:** `import { useTransition } from "react"`
- **Client Component:** Requires `"use client"` since it operates on client-side React state.
- **Synchronous Execution:** The function you pass to `startTransition` must be synchronous. (Though Server Actions, which return promises, are famously integrated closely with `startTransition` in Next.js).
- **Interruptible:** If a more urgent update happens (e.g., the user types into an input), React will interrupt the transition and handle the urgent update first.

## 📦 Return Values `[isPending, startTransition]`
| Property | Type | Description |
| :--- | :--- | :--- |
| `isPending` | `boolean` | `true` if there is a pending transition triggered by `startTransition`. Use this to show a loading state. |
| `startTransition` | `function` | A function that lets you mark one or more state updates as a transition (`startTransition(() => { ... })`). |

## 💻 Example

**Using `useTransition` to Keep the UI Responsive**
```tsx
"use client";
import { useState, useTransition } from "react";
import { searchItems } from "./actions";

export default function SearchWithTransition() {
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);
  
  // 1. Setup the hook
  const [isPending, startTransition] = useTransition();

  const handleChange = (e) => {
    const value = e.target.value;
    
    // Update the input state immediately (urgent)
    setQuery(value);

    // 2. Wrap the less urgent work in startTransition
    // This allows the user to keep typing seamlessly
    // without the UI freezing while loading or calculating.
    startTransition(async () => {
      // In Next.js, tying a Server Action here automatically tracks loading state
      const response = await searchItems(value); 
      setResults(response);
    });
  };

  return (
    <div>
      <input 
        type="text" 
        value={query} 
        onChange={handleChange} 
        placeholder="Type to search..."
      />
      
      {/* 3. Render loading UI using isPending */}
      {isPending && <p>Searching...</p>}
      
      <ul>
        {results.map((item, index) => (
          <li key={index}>{item.title}</li>
        ))}
      </ul>
    </div>
  );
}
```
