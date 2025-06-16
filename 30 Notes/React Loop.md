---
created: 2024-04-23 06:10
modified: 2025-06-15T19:01:21-04:00

---
up::  [[Joy of React]]
source:: [Render and Commit – React](https://react.dev/learn/render-and-commit)
## React Loop
![[Screenshot 2024-06-08 at 6.34.58 PM.png]]
The React loop consists of three stages: Trigger, Render, and Commit. Each stage represents a step in the process of rendering and updating a component in the React framework.

1. **Trigger**: This stage occurs when there is an **event or an update that requires the component to re-render**. This could be a **result of a change in state** or props, or a call to the `forceUpdate` method. The trigger stage sets in motion the process of re-rendering the component.

2. **Render**: During the render stage, React calls the component's `render` method to determine what the updated component should look like. It does this by **comparing the previous and current state** and props of the component through a process known as **reconciliation**. React creates a **virtual DOM** to represent the new component structure and then determines the necessary changes to be made to the **actual DOM.**

3. **Commit**: After the render stage, React is ready to make the updates to the actual DOM. This is known as the commit stage. React applies the changes calculated during the render stage to the DOM. This could include adding, removing, or updating DOM nodes.

In summary, the React loop is a continuous cycle of mounting, triggering, rendering, and committing that ensures the component is always up to date with the latest changes in state or props
