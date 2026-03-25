
### Rendering Strategies Quick Reference

| Type | How it's written (Next.js) | When it runs |
| :--- | :--- | :--- |
| **CSR** | `useEffect` + `'use client'` | In the user's browser |
| **SSR** | `fetch(url, { cache: 'no-store' })` | Every time someone visits (on-demand) |
| **SSG** | `fetch(url)` | Once, during the build process |
| **ISR** | `fetch(url, { next: { revalidate: 60 } })` | In the background every X seconds |