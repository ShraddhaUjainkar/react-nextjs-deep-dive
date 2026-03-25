# `useFormStatus` (Next.js)

`useFormStatus` tracks form submission state (e.g., loading/pending) without needing `useState`.

## 📌 Key Rules
- **Import:** `import { useFormStatus } from "react-dom"`
- **Client Component:** Requires `"use client"`.
- **Child Only:** Must be called in a component rendered *inside* a `<form>`, **not** the component defining the `<form>`.
- **Server Actions:** Only tracks submissions using the `<form action={...}>` prop (not standard `onSubmit` + `fetch` handlers).

## 📦 Return Values
| Property | Type | Description |
| :--- | :--- | :--- |
| `pending` | `boolean` | `true` if form is submitting. |
| `data` | `FormData` | The data being submitted. |
| `method` | `string` | HTTP method used (`GET` or `POST`). |
| `action` | `function` | Reference to the form's `action` function. |

## 💻 Example

**1. Child Component (The Button)**
```tsx
"use client";
import { useFormStatus } from "react-dom";

export function SubmitButton() {
  const { pending } = useFormStatus();

  return (
    <button type="submit" disabled={pending}>
      {pending ? "Submitting..." : "Save Changes"}
    </button>
  );
}
```

**2. Parent Component (The Form)**
```tsx
import { SubmitButton } from "./SubmitButton";
import { updateProfile } from "./actions";

export default function ProfileForm() {
  return (
    <form action={updateProfile}>
      <input type="text" name="username" />
      <SubmitButton /> // <-- Must be a child of the form!
    </form>
  );
}
```