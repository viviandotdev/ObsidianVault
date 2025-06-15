---
created: 2024-03-26 19:53
modified: 2025-06-13T08:15:14-04:00
alias:
---
# How to model a Chair
up::  [[A Complete Guide to 3D Modelling in Blender - Patata School]]
tags:: #blender
links::
## Chair

Parts of a Chair:
1. Seat
2. Backrest
3. Legs
4. Rocking Part
5. Armrests


**Creating the Curved Legs:**
1. Apply the Mirror modifier on the cube.
	- Mirror Modifier: Mirror around the origin point. In edit mode, move the object.
		- Apply Transforms if anything looks weird.

2. Extrude the cube to make it longer.
3. Add a loop cut in the middle to make it a slight, curved U shape.
4. Add a Subdivision Surface modifier and add loop cuts to sharpen edges.
5. Add loop cuts to the bottom face.

**Creating the Front Legs:**
1. Create another cube to create the front legs.
2. Make it long, extrude, and curve it.
3. Add a Subdivision Surface modifier.
4. Add loop cuts to the top and bottom.

**Creating the Back Legs:**
1. Duplicate and move the front legs to the back.
2. Move up the face to elongate.
3. Scale the base larger.
4. Scale the curved edges larger.
5. Add the Mirror modifier to the legs.

**Creating the Seat Edges:**
1. Duplicate the front legs.
2. Move and rotate them to make the seat edges.
3. Extend the faces.
4.
**Creating the Seat Base:**
1. Remove the Mirror modifier from the arms.
2. Duplicate the single arm.
3. Scale horizontally to create the seat base.
4. Add loop cuts to all edges.
5. Move into position.

**Creating the Spherical Details:**
1. Create a sphere with 18 segments and 10 rings.
2. Add a Subdivision Surface modifier.
3. Place the cubes at the top.

**Creating the Backrest:**
1. Create a cube.
2. Apply an Array modifier vertically.
3. Rotate and scale the backrest into place.
4. Add a Bevel modifier with a value of 2.

**Modifiers Used**
 Mirror modifier
 Subdivision Surface modifier
 Array modifier
 Bevel modifier
 ![[Screenshot 2024-03-20 at 7.33.15 PM.png]]
