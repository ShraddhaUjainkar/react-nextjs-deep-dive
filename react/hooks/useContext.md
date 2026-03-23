
# useContext Hook

`useContext` is used to access **global data** without passing props manually through many components.

This avoids **prop drilling**.

---

## Example

### Create Context

```javascript
import { createContext } from "react";

export const UserContext = createContext();
```
### Provide Context
```javascript
<UserContext.Provider value="Shraddha">
  <Child />
</UserContext.Provider>
```

### Consume Context
```javascript
import { useContext } from "react";
import { UserContext } from "./UserContext";

function Child() {
  const user = useContext(UserContext);

  return <h1>{user}</h1>;
}
```
    