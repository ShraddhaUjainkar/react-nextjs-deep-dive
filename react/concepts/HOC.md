Markdown
# React Higher-Order Components (HOC)

An **HOC** is a function that takes a component and returns a new component, primarily used for **reusing logic**.

---

## Pattern
```javascript
const NewComponent = withLogic(BaseComponent);
Basic Example: withLoading
This HOC displays a spinner if the isLoading prop is true.

JavaScript
const withLoading = (Component) => {
  return ({ isLoading, ...props }) => {
    if (isLoading) return <div>Loading...</div>;
    return <Component {...props} />;
  };
};

export default withLoading;
```

## Quick Rules
- Don't Mutate: Return a new component, don't modify the original.
- Pass Props: Use {...props} to ensure the wrapped component receives its data.
- Define Outside: Never create an HOC inside a render method; it causes unnecessary unmounts.
- Static Methods: They aren't automatically copied to the new component.

## HOC vs. Hooks
- HOCs: Great for UI/Layout wrappers and legacy Class Components.
- Hooks: Generally preferred for data/state logic in Functional Components.

# Auth HOC Example

```jsx
import React from 'react';
import { Redirect } from 'react-router-dom';

const withAuth = (WrappedComponent) => {
  return (props) => {
    const isAuthenticated = localStorage.getItem('token');

    if (!isAuthenticated) {
      return <Redirect to="/login" />;
    }

    return <WrappedComponent {...props} />;
  };
};

export default withAuth;

const Dashboard = () => <div>Sensitive Data</div>;

// Only logged-in users can see this
export default withAuth(Dashboard);
```