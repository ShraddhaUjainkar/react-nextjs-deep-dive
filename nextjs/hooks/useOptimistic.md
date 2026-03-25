# `useOptimistic` (React / Next.js)

`useOptimistic` lets you optimistically update the UI before an asynchronous operation (like a Server Action) finishes. It provides a fast, responsive user experience without having to wait for the server roundtrip.

## 📌 Key Rules
- **Import:** `import { useOptimistic } from "react"`
- **Client Component:** Requires `"use client"` since it manages UI state changes on the client side.
- **Automatic Reversal:** The optimistic state is temporary. It will automatically revert to the underlying real server state when the Server Action finishes (successfully or if it throws an error).

## 📦 Arguments & Return Values

### Arguments `useOptimistic(state, updateFn)`
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `state` | `any` | The initial, actual underlying state (often passed down from a Server Component or a data fetch). |
| `updateFn` | `function` | A reducer function: `(currentState, optimisticValue) => newState`. It computes the temporary optimistic state based on the current state and the exact value you pass to update it. |

### Returns `[optimisticState, addOptimistic]`
| Property | Type | Description |
| :--- | :--- | :--- |
| `optimisticState` | `any` | The state value you should render in your UI. This matches `state` normally, but matches the result of `updateFn` momentarily while an action is pending. |
| `addOptimistic` | `function` | The dispatch function you call with your `optimisticValue` to immediately trigger the optimistic UI change. |

## 💻 Example

**Optimistic Task List**
```tsx
"use client";
import { useOptimistic } from "react";
import { addTask } from "./actions";

export default function TodoList({ tasks }) {
  // 1. Setup the hook
  const [optimisticTasks, addOptimisticTask] = useOptimistic(
    tasks, // The real server state
    (currentTasks, newTaskName) => [
      ...currentTasks, 
      { name: newTaskName, pending: true } // How to append the new item optimistically
    ]
  );

  return (
    <div>
      {/* 2. Render from optimisticTasks, NOT the original tasks */}
      <ul>
        {optimisticTasks.map((task, index) => (
          <li key={index} style={{ opacity: task.pending ? 0.5 : 1 }}>
            {task.name} {task.pending && "(Saving...)"}
          </li>
        ))}
      </ul>

      {/* 3. Wrap your Server Action execution inside your form or event handler */}
      <form action={async (formData) => {
          const newTaskName = formData.get("taskName");
          
          // Fire the optimistic update immediately
          addOptimisticTask(newTaskName);
          
          // Then actually hit the server via Server Action
          await addTask(formData);
      }}>
        <input type="text" name="taskName" required />
        <button type="submit">Add Task</button>
      </form>
    </div>
  );
}
```
