What are React Server Components (RSC)

React Server Components run only on the server and their JavaScript is never sent to the browser.

They allow React applications to reduce the amount of JavaScript sent to the client.

RSC Flow
User Request
     ↓
Server runs Server Components
     ↓
Fetches data
     ↓
Server sends serialized UI tree
     ↓
Browser renders minimal JavaScript