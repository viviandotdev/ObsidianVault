---
created: 2023-09-21 15:06
modified: 2025-06-16T08:33:27-04:00
---
up::  [[+ 3JS-Three.js Journey]]
## Optimizing a 3D Model

1. Removes all the faces you cannot see
2. Unlink duplicates
	1. If we keep the links such as the pole light, both lights would be unwrapped on the same coordinates. This will result in baking being done twice in the same position of the texture
	2. To unlink duplicates, select all options, open the search menu to find `Make Single User > Object & Data`
3. Normalize the scales
	Objects have to be scaled in `Edit mode` so that we are scaling the geometry and not the object itself. When objects are scaled in `Object Mode` the transformation is on the object but not the geometry itself. This creates issues when doing the UV unwrapping because blender takes into account the geometry size but not the object size. Therefore, this may result in objects take more space or not as much as they should

	In `Object Mode`, select all the objects with `A` , press `CTRL + A` to open the `Apply` menu and choose `Scale`:
4. Fix the face orientation
	All faces have a front and back. By default, back faces won't be rendered in the baking process because they are hidden and will become black.
	- Check `Face Oreintation` in the `Viewport Overlays` this will show all the objects with back faces
	- Select the red faces of the objects you want to fix
		- Go into `Edit Mode`
		- Select the face to flip
		- In the search menu find `Mesh > Normals > Flip`
		- Or you can also select the entire object and then in the search menu find `Mesh > Noramsl > Recalculate Outside`


### Resources
[Three.js Journey — Baking and exporting the scene](https://threejs-journey.com/lessons/baking-and-exporting-the-scene#fixing-faces-orientation)
