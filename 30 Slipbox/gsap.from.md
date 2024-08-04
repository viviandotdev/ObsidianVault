---
created: 2024-01-25 12:48
modified: Thursday 25th January 2024 12:48:57
alias:
---
up::
tags:: #gsap

## gsap.from

The animation **starts from the values specified in the vars parameters** and animates **toward the current properties already set in the css/html.**
Used for animating objects onto the screen
You can set up how to want then to look on the screen and then animate them toward that position from elsewhere.

Lets say you want a text to drop in to the screen, you can set the text to where you want it to be on the screen and set the `gsap.from("h1", { y: -200, duration: 2 });` so the text is outside the screen and drop into the end position.
[Code Example](https://github.com/designcourse/af-project-files/blob/main/2%20-%20GreenSock/1%20-%20From%20and%20To%20Method/After/index.html#L22)

```ts
// animate ".class" from an opacity of 0 and a y position of 100 (like transform: translateY(100px))
// to the current values (an opacity of 1 and y position of 0).
gsap.from(".box", { opacity: 0, y: 100, duration: 1 });
```

This would animate the element with the class "box" from an opacity of 0 and y position of 100 to its current values.

[gsap.from() | GSAP | Docs & Learning](https://gsap.com/docs/v3/GSAP/gsap.from())
