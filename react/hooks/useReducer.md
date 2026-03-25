# `useReducer` (React)

`useReducer` is a React Hook for complex state management. It is preferable to `useState` when state logic is complex, when multiple state values depend on each other, or when the next state heavily depends on the previous one. It offers predictable state transitions using a structured, Data Structures & Algorithms (DSA)-style approach: **Input (Action) → Processing Function (Reducer) → New State (Output)**.

## 🧠 DSA-Style Thinking
Think of it like applying an algorithm to a data structure:
- **State:** The current data structure (e.g., array or object).
- **Action:** The operation to perform (e.g., insert, delete, update).
- **Reducer:** The function that contains the logic to apply the action.
- **Dispatch:** The command to trigger the operation.

## 🏗️ Syntax & Arguments

```tsx
const [state, dispatch] = useReducer(reducer, initialState);
```

### Arguments `useReducer(reducer, initialState)`
| Parameter | Type | Description |
| :--- | :--- | :--- |
| `reducer` | `function` | The logic handler function: `(state, action) => newState`. |
| `initialState` | `any` | The starting value for your state data structure. |

### Returns `[state, dispatch]`
| Property | Type | Description |
| :--- | :--- | :--- |
| `state` | `any` | The current state value. |
| `dispatch` | `function` | A function used to send (dispatch) actions to the reducer. |

## 🔄 The Flow
1. An event occurs (e.g. button click) and calls: `dispatch({ type: "increment" })`
2. React automatically calls: `reducer(state, action)`
3. The `reducer` returns the **new state**.
4. React **re-renders** the component with the updated state.

## 💻 Examples

### 1. Basic Example: Counter

```tsx
import { useReducer } from "react";

// Step 1: Define the Reducer Function
function reducer(state, action) {
  switch (action.type) {
    case "increment": 
      return { count: state.count + 1 };
    case "decrement": 
      return { count: state.count - 1 };
    default: 
      return state;
  }
}

// Step 2: Use in Component
export default function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <h1>{state.count}</h1>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
    </div>
  );
}
```

### 2. Real-Life Example: Todo App Array Logic

```tsx
function todoReducer(state, action) {
  switch (action.type) {
    case "add":
      // Appending to an array (DSA "Insert")
      return [...state, action.payload];
      
    case "delete":
      // Removing from an array (DSA "Delete")
      return state.filter((todo, index) => index !== action.index);
      
    default:
      return state;
  }
}
```