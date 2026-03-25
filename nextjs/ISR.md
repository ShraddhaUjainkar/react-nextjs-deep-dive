##  Incremental Static Regeneration (ISR)

- ISR looks exactly like SSG, but you add a next.revalidate property. This tells the server: "Keep this static, but refresh it in the background at most every 60 seconds."

```javascript
export default async function IsrPage() {
  // Re-generate this page if a request comes in and 
  // it has been more than 60 seconds since the last update
  const res = await fetch('https://api.example.com/data', {
    next: { revalidate: 60 },
  });
  const data = await res.json();

  return (
    <main>
      <h1>Incremental Static Regeneration</h1>
      <p>Last updated: {new Date().toLocaleTimeString()}</p>
      <p>{data.message}</p>
    </main>
  );
}   
```