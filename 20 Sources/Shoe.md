---
created: 2024-03-26 18:24 
modified: Tuesday 26th March 2024 18:24:25
alias: 
---
up::  [[A Complete Guide to 3D Modelling in Blender - Patata School]]
tags::  
links::  
## Shoe  


**Table of Contents**
- [[#Boot|Boot]]
- [[#Shoe Lace|Shoe Lace]]

#### Boot

1. Sole of the boot  
	![[Screenshot 2024-03-23 at 10.34.00 AM 4.png]]  
2.   Duplicate sole and move the top face up and adjust  
	![[Screenshot 2024-03-23 at 10.35.24 AM.png]]  
3. Make loop cuts into the boot shape  
4. Inset the top of the boot and extrude downwards  
	![[Screenshot 2024-03-23 at 10.36.07 AM.png]]  
5. Final boot  
 ![[Screenshot 2024-03-23 at 10.37.40 AM.png]]  



#### Shoe Lace

1. Create a bezier and circle curve
	![[Screenshot 2024-03-23 at 10.40.21 AM.png]]
		1. Scale the point to make the line wider or taller
2. Select curve select object path, -> bevel -> object and for the object select the bezier circle
	This create a 3D curve with the circle as the geometry
	![[Fill Caps.png]]
3. Attach the shoe lace to the shoe
4. Create a torus- Medial radius-0.44mm
5. Use mirror modifier, to create the shoelace metal part

**Side Strap**
1. Duplicate the **Boot**
2. Apply the subdivision surface to the boot
3. Select the strap part 
	1. **Alt Select** to Create the loop
	2. **CTRL select** to remove selection
	3. ![[Screenshot 2024-03-23 at 10.47.48 AM.png]]
4.  Then  select -> invert then delete, remove the boot except for the strap
5. Apply solidify modifier to add thickness to the strap
6. Add bevel modifier 7  segments
7. Duplicate the lace and. Finalize the shoe
![[Screenshot 2024-03-23 at 10.50.20 AM.png]]