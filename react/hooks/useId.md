## useId

- The useId hook generates unique IDs for elements within a component, which is crucial for accessibility by dynamically creating ids that can be used for linking form inputs and labels. It guarantees unique IDs across the application even if the component renders multiple times.

```jsx      
import { useId } from 'react';

function MyComponent() {
  const id = useId();

  return (
    <div>
      <label htmlFor={id}>Name:</label>
      <input id={id} type="text" />
    </div>
  );
}   
```

## Key Points

- **Uniqueness**: The ID is unique across the entire application, even if the component renders multiple times.
- **Server-Side Rendering**: The ID is the same on both the server and the client, which is crucial for Server-Side Rendering (SSR).
- **No Collisions**: It avoids ID collisions when rendering multiple instances of the same component.
- **Accessibility**: It is primarily used for accessibility purposes, such as linking form inputs and labels.

