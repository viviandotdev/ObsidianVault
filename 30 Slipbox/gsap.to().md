---
created: 2024-01-25 12:45
modified: Thursday 25th January 2024 12:45:16
alias:
---
up::
tags:: #gsap

## gsap.to()

1. **targets** - the object(s) whose properties you want to animate. This can be selector text like `".class"`, `"#id"`, etc. (GSAP uses [`document.querySelectorAll()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll) internally) or it can be direct references to elements, generic objects, or even an array of objects.
2. **vars** - an object containing all the properties/values you want to animate, along with any special properties like `ease`, `duration`, `delay`, or `onComplete` (listed below).

The animation **starts from the current properties in the css/html** of the target and **animates towards the values specified in the  vars parameters of the function**



```ts
// rotate and move elements with a class of "box"
// ("x" is a shortcut for a translateX() transform) over the course of 1 second.
gsap.to(".box", { opacity: 1, x: 100, duration: 1 });
```

This would animate the element with the class "box" from its current opacity and x position **to an opacity of 1 and x position of 100.**

### Resources

[gsap.to() | GSAP | Docs & Learning](https://gsap.com/docs/v3/GSAP/gsap.to())
