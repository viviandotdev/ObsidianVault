---
created: 2024-01-26 16:46
modified: Friday 26th January 2024 16:46:40
alias:
---
up::
tags:: #gsap

## gsap.scrollTrigger()



ScrollTriggers performs animations on object when entering or leaving a defined area that is linked to the scrollTrigger.
Only plays when the target element is in the view port
**Example**
```ts
  scrollTrigger: {
        trigger: "section.details",
        start: "top bottom", // when trigger starts
        end: "bottom top",
        scrub: true,
        markers: true,
  },
```

### Properties
`start` determines the starting point of the Scroll Trigger
	`"top center"` means _"when the top of the trigger element hits the center of the scroller (viewport)"_
		the first value indicates the start position of the trigger element and second indicates the position of the scroller (default- viewport)



[[gsap.scrollTrigger.toggleActions|toggleActions]] is ScrollTrigger property that **lets you control the playback** of your animation during 4 stage

#### Resources
Tutorial
[ScrollTrigger | GSAP | Docs & Learning](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)
[Code Pen DEMO](https://codepen.io/GreenSock/pen/RwPXQOQ)
[GSAP ScrollTrigger - YouTube](https://www.youtube.com/playlist?list=PLMPgoZdlPumexxtvuPUB3TY7LExI1N_Xp)

Examples
[GSAP And GSAP ScrollTrigger - YouTube](https://www.youtube.com/playlist?list=PLZ44pviE5AD2uHCmUx9CCiioQfCpkjIna)
