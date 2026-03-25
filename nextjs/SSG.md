## Static Site Generation (SSG)

For SSG, the framework fetches the data once during the build process and keeps it as a static file. In Next.js, this is the default behavior for fetch if you don't provide extra options.

```javascript
export default async function StaticPage() {
  // This fetch happens once at build time
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return (
    <main>
      <h1>Static Site Generation</h1>
      <p>{data.message}</p>
    </main>
  );
}   
```