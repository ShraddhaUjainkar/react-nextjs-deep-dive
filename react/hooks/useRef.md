# useRef Hook

## What is useRef?

useRef is a React hook used to store a mutable value that does not trigger a re-render when updated.

- Stores a mutable value
- Does NOT trigger re-render
- Can reference a DOM element

## Syntax

const ref = useRef(initialValue)

## Example

function Example() {
const inputRef = useRef()

const focusInput = () => {
inputRef.current.focus()
}

return (
<>
<input ref={inputRef} />
<button onClick={focusInput}>Focus</button>
</>
)
}

## When to Use

- Access DOM elements
- Store previous state
- Store timers or interval IDs

## Interview Question

Why doesn't useRef trigger re-render?

useRef doesn’t trigger a re-render because updating ref.current does not change React state. React only re-renders when state or props change, not when a ref value changes.

- useRef = store value without causing re-render.
