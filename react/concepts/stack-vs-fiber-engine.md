## Overview of Engine

1. The Engines

- Previous Engine: Stack Reconciler (Used in React 15 and below).

- Current Engine: Fiber Reconciler (Introduced in React 16+).

2. How it Worked vs. How it Works Now
   | Feature        | Previous (Stack)                                                              | Now (Fiber)                                                                      |
   | -------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
   | Data Structure | Uses the Call Stack (Recursion).                                              | Uses Linked Lists (Individual units of work).                                    |
   | Execution      | Synchronous: Once it starts, it cannot stop until the whole tree is finished. | Asynchronous: It can pause, resume, or discard work as needed.                   |
   | Main Thread    | Blocks the thread. If the tree is huge, the UI freezes until rendering ends.  | Yields to the thread. It "checks in" with the browser to keep animations smooth. |
   | Prioritization | Every update has the same importance.                                         | Supports Priorities. Clicks and typing jump to the front of the line.            |
   | Updates        | Updates the DOM in one giant leap.                                            | Breaks work into small chunks (Incremental Rendering).                           |
