---
created: 2024-03-26 19:53
modified: 2025-06-13T08:15:14-04:00

---
# How to model a House
up::  [[3DM-A Complete Guide to 3D Modeling in Blender - Patata School]]
tags::
source::
## House

1. Create cube, platform
	Add bevel, to soften shape of the platform![[Screenshot 2024-03-28 at 9.04.41 PM.png]]
2. L shape
	1. Create a plane
	2. extrude the back and move it along the y slightly
	3. Add bevel. modifier to the plane to curve the shape
		![[Screenshot 2024-03-28 at 9.06.05 PM.png|400]]
3. House References, make sure to move the base instead of the house, so the house is always centered
	 ![[Screenshot 2024-03-28 at 9.08.19 PM.png|400]]
4. Trucks
	1. Create cylinder
	2. Rotate in x 90
	3. Scale to size
	4. Add bevel and Add array modifier, on the y to 5.
	5. Apply all transforms
	6. Then apply mirror modifier.
	7. Then duplicate,
	8. And rotate to the front of the house and then scale on the x![[Screenshot 2024-03-28 at 9.12.02 PM.png]]
	9. Apply mirror again for the back![[Screenshot 2024-03-28 at 9.12.40 PM.png]]
5. Create a cylinder for the columns
	1. Add bevel, shade smooth and the create second column
		 ![[Screenshot 2024-03-28 at 9.14.36 PM.png|200]]

6. Create wooden panels
	1. Create cube and scale in to panel shape
		1. add the bevel modifier
		2. apply all transforms
		3. shade smooth
		4. Apply mirror modifier
		5. ![[Screenshot 2024-03-28 at 9.16.54 PM.png|200]]
		6. Shift D to Duplicate the panels, to into edit mode and move the points down
		1. ![[Screenshot 2024-03-28 at 9.17.31 PM.png]]
7. Create cube for the roof panels
	1. Add bevel modifier
	2. Add the array modifier on the y, 6 items
	3. Add another array modifier ( add a small factor to offset them)
	4. Then. rotate on the shape of the roof.
	![[Screenshot 2024-03-28 at 9.20.05 PM.png|150]]![[Screenshot 2024-03-28 at 9.20.26 PM.png|400]]
5. Then copy and then rotate Z 180 degrees
	 ![[Screenshot 2024-03-28 at 9.21.55 PM.png]]
7. Make Stairs
	1. Duplicate the front logs
	2. Change to 3
	3. update the factor to offset them![[Screenshot 2024-03-28 at 9.22.56 PM.png]]
8. Create door, shape into door, add bevel
	1. ![[Screenshot 2024-03-28 at 9.24.31 PM.png|100]]
	2. Create windows, create a new object for the holes in the door
	3. Then add array modifiers
	4. ![[Screenshot 2024-03-28 at 9.25.31 PM.png|200]]
	5. Add and apply the boolean modifier to the door
	6. Add handle and bottom panels
	![[Screenshot 2024-03-28 at 9.28.00 PM.png|200]]
9.  Create the. mat
	1. Duplicate one of the bottom panels
10. Chimney
	1. Create cube, add the bevel modifier
	2. Duplicate scake z and them scale widier
	3. Inset and extrude down
		 ![[Screenshot 2024-03-28 at 9.30.09 PM.png|200]]

Rearrange the bojects into space
1. To scale properly to make sure to deselect the belt shape, arm shapes, and leg shapes and the shoelace shapes
2.  ![[Screenshot 2024-03-28 at 9.32.06 PM.png]]
3.
Put everything into place
![[Screenshot 2024-03-30 at 11.41.50 AM.png]]
