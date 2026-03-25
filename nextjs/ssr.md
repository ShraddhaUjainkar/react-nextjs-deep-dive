# React Server Components (RSC) vs Server-Side Rendering (SSR)

In modern React frameworks like Next.js, both **React Server Components (RSC)** and **Server-Side Rendering (SSR)** involve server-side execution. However, they solve different problems and work differently.

In the App Router, components are Server Components by default. To achieve SSR (fetching fresh data on every request), you disable caching in your fetch request.

```javascript
export default async function ServerPage() {
  // { cache: 'no-store' } forces the server to fetch on every request
  const res = await fetch('https://api.example.com/data', { cache: 'no-store' });
  const data = await res.json();

  return (
    <main>
      <h1>Server-Side Rendered</h1>
      <p>{data.message}</p>
    </main>
  );
}
```

# 1. What is Server-Side Rendering (SSR)

Server-Side Rendering means the **server generates HTML for a page on every request** and sends it to the browser.

After the HTML loads, React **hydrates** the page to make it interactive.

## SSR Flow
User Request
↓
Server renders React components
↓
HTML sent to browser
↓
Browser downloads React JavaScript
↓
Hydration happens
↓
Page becomes interactive





## Example (Next.js SSR)

```javascript
export async function getServerSideProps() {
  const res = await fetch("https://api.example.com/data")
  const data = await res.json()

  return {
    props: { data }
  }
}

export default function Page({ data }) {
  return <div>{data.title}</div>
}