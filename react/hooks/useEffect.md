
# useEffect Hook

`useEffect` is used for **side effects** in React components.

Examples of side effects:

- API calls
- Timers
- DOM updates
- Event listeners

---

## Syntax

```javascript
useEffect(() => {
  // code
}, [dependencies])
``` 

- Run Once (componentDidMount)
```javascript

useEffect(() => {
  console.log("Component Mounted");
}, []);
```

- Run on Dependency Change
```javascript
useEffect(() => {
  console.log("Count changed");
}, [count]);
```


- Cleanup Function (componentWillUnmount)
```javascript
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Running");
  }, 1000);

  return () => {
    clearInterval(timer);
  };
}, []);         
```

