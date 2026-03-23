 # What are the recommended ways for type checking of React component props?

## 📌 Overview

The recommended ways for static type checking in React are:

## 1. TypeScript:
 A superset of JavaScript that adds optional static typing. It provides strong type checking, autocompletion, and other benefits at development time.

```javascript
interface MyComponentProps {
  name: string;
  age: number;
}

function MyComponent({ name, age }: MyComponentProps) {
  return <div>{name} is {age} years old</div>;
}
```

## 2. PropTypes: 
A runtime type-checking tool for React props, primarily for development purposes. It helps catch errors by checking prop types during development but doesn't offer full static analysis like TypeScript.

```javascript
import PropTypes from 'prop-types';

function MyComponent({ name, age }) {
  return (
    <div>
      {name} is {age} years old
    </div>
  );
}

MyComponent.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
};
```
TypeScript is the preferred choice for static type checking due to its integration with the build process and comprehensive tooling, whereas PropTypes is useful for smaller projects or when you need runtime checks.

