---
created: 2024-01-25 14:02
modified: Thursday 25th January 2024 14:02:36
alias:
---
up::
tags:: #gsap

## gsap.timeline()



[Timeline | GSAP | Docs & Learning](https://gsap.com/docs/v3/GSAP/Timeline/)


Timeline is a sequencing tool that acts as a container for tweens to make it easier to control their timing.

```ts
// WITHOUT Timelines (only using tweens with delays):
gsap.to("#id", { x: 100, duration: 1 });
gsap.to("#id", { y: 50, duration: 1, delay: 1 }); //wait 1 second
gsap.to("#id", { opacity: 0, duration: 1, delay: 2 }); //wait 2 seconds
```


```ts
//WITH Timelines (cleaner, more versatile)
// Timeline defaults aplly to all tweens in the timeline
// Repeats the whole animation sequence twice with a 1 second delay between the respts
var tl = gsap.timeline({defaults: { ease: "power4.inOut", duration: 1 }, repeat: 2, repeatDelay: 1});
tl.to("#id", {x: 100 });
tl.to("#id", {y: 50 });
tl.to("#id", {opacity: 0 });

// then we can control the whole thing easily...
tl.pause();
tl.resume();
tl.seek(1.5);
tl.reverse();
...
```

We can use the **position parameter** to control where things are placed in the timeline

```ts
// insert exactly 3 seconds from the start of the timeline
tl.to(".class", { x: 100 }, 3)
// 1second before the end of the timeline (overlaps)
tl.to(".class", { x: 100 }, "+=1);
// insert at the "someLabel" label
tl.to(".class", { x: 100 }, "someLabel");
// insert at the END of the previous animation
tl.to(".class", { x: 100 }, ">");
```

- `"+=1"` - 1 second past the end of the timeline (creates a gap)
- `"-=1"` - 1 second before the end of the timeline (overlaps)
- `"myLabel+=2"` - 2 seconds past the label `"myLabel"`
- `"<+=3"` - 3 seconds past the start of the previous animation
