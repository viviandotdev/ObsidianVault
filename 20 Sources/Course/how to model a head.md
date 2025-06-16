---
created: 2024-03-26 19:53
modified: 2025-06-15T19:13:23-04:00

---
# How to model a Head
up::  [[A Complete Guide to 3D Modelling in Blender - Patata School]]
tags::
source::
## Head

Tip
- Reduce the number of cuts

****
1. Create Cube
2. Subdivision surface 2, 2 and
3. Duplicate the cube
	1. flatten to make muzzle
4. Create cube
	1. Scale down for the nose
	2. Apply subdivision surface
	3. Add loop cut to the top
	4. Scale to flatten
	5. Scale X the bottom face of nose
	![[Screenshot 2024-03-26 at 6.42.10 PM.png|250]]
5. Eyes: Create a sphere for the eyes
	1. Apply the **mirror modifier**
6. Eyebrows
	1. Create cube
	2. Apply subdivision modifier
	3. Add loop cuts
	 ![[Screenshot 2024-03-26 at 6.43.58 PM.png]]
	4. rotate and scale eyebrows into place
	 ![[Screenshot 2024-03-26 at 6.45.09 PM.png|300]]
7. Mouth
	1. Create cube and extrude into mouth
	 ![[Screenshot 2024-03-26 at 6.47.48 PM.png|300]]
	 2. Add the subdivision surface
		 ![[Screenshot 2024-03-26 at 6.49.53 PM.png]]
8. Ears
	1. Create cube
	2. Scale Y
	3. Loop cuts, then apply subdivision surface
		![[Screenshot 2024-03-26 at 6.51.10 PM.png|400]]
	4. Select bottom two face, move back, scale
		![[Screenshot 2024-03-26 at 6.52.31 PM.png|300]]
	5.  move ears into place and apply the mirror
		![[Screenshot 2024-03-26 at 6.54.36 PM.png]]
9. Hat
	1. Cube and scale flat for hat base
		1. Add subdivision modifier
		2. Add loop cuts to sharpen the hat
		3. ![[Screenshot 2024-03-26 at 6.56.24 PM.png]]
	2. Hat top
		1. Create cube add subdivision modifier
		2. Add loop cut to bottom
			1. add loopo cuts to middle and top middle
			2. ![[Screenshot 2024-03-26 at 6.58.26 PM.png]]
		3. Play the object and morph it into a shape of a hat![[Screenshot 2024-03-26 at 7.00.20 PM.png]]!
10. Organize the objects and place in collection called **Head**
**Final Bear**
![[Screenshot 2024-03-26 at 7.00.52 PM.png]]
