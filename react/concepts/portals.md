## Overview

React Portals allow rendering children into a DOM node outside the parent component's hierarchy. This is useful for modals or tooltips that need to escape parent overflow or z-index constraints.

## How it works

 - `ReactDOM.createPortal(child, container)`: Creates a portal that renders `child` into `container`.
 - The portal maintains the parent's event-bubbling behavior, meaning events from the portal's children will still bubble up to the parent component.

 ## Example

 ```jsx
 import ReactDOM from 'react-dom';

 function Modal({ children }) {
   return ReactDOM.createPortal(
     <div className="modal">{children}</div>,
     document.body
   );
 }
 ```

 ## Key Points

 - Portals maintain the parent's event-bubbling behavior.
 - Portals can be used to render children into a DOM node outside the parent component's hierarchy.
 - Portals are useful for modals or tooltips that need to escape parent overflow or z-index constraints.
 