## Client-Side Rendering (CSR)

- In modern frameworks, you opt into CSR by using the 'use client' directive. The data fetching usually happens inside a useEffect hook.

```javascript
'use client';

import { useState, useEffect } from 'react';

export default function ClientPage() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then((res) => res.json())
      .then((data) => setData(data));
  }, []);

  if (!data) return <p>Loading...</p>;
  return <div>{data.message}</div>;
}
```