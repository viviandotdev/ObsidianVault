---
created: 2024-01-25 13:10
modified: Thursday 25th January 2024 13:10:28
alias:
---
up::
tags:: #gsap

## gsap.set()



Sets the properties of a target, a 0 duration [[gsap.to()]]

Below each does the same
```ts
gsap.set(".class", { x: 100, y: 50, opacity: 0 });
gsap.to(".class", { duration: 0, x: 100, y: 50, opacity: 0 });
```


Array to select and set multiple target at once
```ts
gsap.set([obj1, obj2, obj3], { x: 100, y: 50, opacity: 0 });
```
