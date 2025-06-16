---
created: 2024-04-06 19:46
modified: Saturday 6th April 2024 19:46:59

---
up::  [[FDM-Making Food and Drinks in Blender]]
tags::  [[blender]]
source::
## Liquid


1. Move the cup into position
2. Duplicate the cup,
	1. select the top, then delete the faces
	2. remove soldifiy,
	3. close the face, Face -> Grid Fill
	4. Shade smooth
		![[Screenshot 2024-04-06 at 7.57.55 PM.png]]

4. Create a plane
	1. Add subdivision surface (5, 5),
	2. Add the wave modifier to create a wave
	3. ![[Screenshot 2024-04-06 at 7.59.23 PM.png]]
5. Add modifier solidify
		![[Screenshot 2024-04-06 at 8.00.00 PM.png]]
6. Apply boolean modifier to the liquid, and select the intersection of liquid and the liquid cutting reference(wave)
![[Screenshot 2024-04-06 at 8.02.04 PM.png|300]]
7. Rotate the the lib open
8. Create the stage
9. Select the bubble and a keyframe in the Z
		![[Screenshot 2024-04-06 at 8.05.12 PM.png|300]]
1. Graph editor
	 in the graph editor add **noise modifier** to, modify the z location in an animation
	![[Screenshot 2024-04-06 at 8.07.31 PM.png]]

	Go back to timeline to play the animation
	![[Screenshot 2024-04-06 at 8.08.07 PM.png]]
2. Apply to all the circles
