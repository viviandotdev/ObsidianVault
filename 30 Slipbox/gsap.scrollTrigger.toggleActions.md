---
created: 2024-02-08 16:00
modified: Thursday 8th February 2024 16:00:44
aliases:
  - toggleActions
---
up::  [[gsap.scrollTrigger()]]
tags:: 
links::
## gsap.scrollTrigger.toggleActions



Determines how the linked animation is controlled at the 4 distinct toggle places - 
**onEnter**- entering the trigger. (*scrolling down*, start and scroller-start meet)
**onLeave**- leaving the trigger going down.  (*scrolling down* end and scroller-end meet)
**onEnterBack**- entering **back up** into the trigger. *scrolling up* scroller end and end meet
**onLeaveBack**- leave by scrolling all the way **back up** past the start (*scrolling up* start and scroller start meet)

play the. animation when entering, pause the animation when leaving, resume when entering again backwards. 


 So `toggleActions: "play pause resume reset"` will play the animation when entering, pause it when leaving, resume it when entering again backwards, and reset (rewind back to the beginning) when scrolling all the way back past the beginning. You can use any of the following keywords for each action: "play", "pause", "resume", "reset", "restart", "complete", "reverse", and "none".