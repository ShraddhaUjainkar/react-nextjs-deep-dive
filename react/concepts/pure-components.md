# What are Pure Components?

## 📌 Overview
Pure Components in React are components that only re-render when their props or state change. They use shallow comparison to check if the props or state have changed, preventing unnecessary re-renders and improving performance.

- Class components can extend React.PureComponent to become pure
- Functional components can use React.memo for the same effect

### Example 
```javascript
const PureFunctionalExample = React.memo(function ({ value }) {
  return <div>{value}</div>;
}); 
```

## React.memo Guide
React.memo is a Higher Order Component (HOC) used to optimize performance by memoizing the rendered output of a component. If your component renders the same result given the same props, React will skip the rendering process and reuse the last rendered result.

### How It Works
By default, React re-renders a child component every time its parent re-renders. React.memo changes this behavior by performing a Shallow Comparison of the props.

- Check: Are the prevProps and nextProps the same?
- Match: Skip re-render, use the cached (memoized) version.
- Mismatch: Re-render the component.

### Basic Syntax
```javascript
import React from 'react';

const MyComponent = React.memo(function MyComponent(props) {
  console.log("Rendering MyComponent...");
  return <div>{props.value}</div>;
}); 

export default MyComponent;
```

### The Shallow Comparison "Gotcha"
As we discussed, React.memo only does a shallow check. If you pass an object, array, or function defined inside a parent component, the reference changes on every render, breaking the memoization.

#### The Problem:
```javascript
// Inside Parent
const Parent = () => {
  // New reference created every time Parent renders!
  const userInfo = { name: "Alex" }; 

  return <MyComponent user={userInfo} />; 
};
```

#### The Solution:
```javascript
// Inside Parent
const Parent = () => {
  const userInfo = useMemo(() => ({ name: "Alex" }), []);
  const handleClick = useCallback(() => console.log("Hi!"), []);

  return <MyComponent user={userInfo} onClick={handleClick} />;
};
```

### Custom Comparison Function
Sometimes you want more control. You can pass a second argument to React.memo to define your own comparison logic (like a deep comparison).Note: This is the opposite of shouldComponentUpdate. Here, returning true means the props are equal and it should NOT re-render.
```javascript
function areEqual(prevProps, nextProps) {
  // Only re-render if the ID changes, ignore other prop changes
  return prevProps.user.id === nextProps.user.id;
}   
```

export default React.memo(MyComponent, areEqual);

### When to Use It?
Don't wrap every component in memo! It carries a memory overhead.

#### ✅ Use it when...
- Component is Pure (same props = same UI)
- Component is simple/cheap to render
- Component renders often with the same props

#### ❌ Avoid it when...
- Props change nearly every time the parent renders
- The render logic is computationally expensive
- The component uses props.children (references change frequently)