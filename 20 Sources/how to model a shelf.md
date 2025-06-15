---
created: 2024-03-26 19:53
modified: 2025-06-13T08:15:14-04:00
alias:
---
# How to model a Shelf
up::  [[A Complete Guide to 3D Modelling in Blender - Patata School]]
tags::
links::
## Log Shelf

# Supporting Text Documentation

## Shelf Construction

### Log Shelf

#### Shelf Structure
- **Create the sides of the shelf:**
  1. Create a cube and scale it to form the sides of the shelf.
  2. Apply a bevel to the cube edges to create a sharp look.
  3. Add a mirror modifier along the Y-axis for symmetry.
- **Create the surface and bottom parts:**
  4. Duplicate the cube and rotate it horizontally to form the top and bottom of the shelf.
  5. Mirror the duplicated cubes along the Z-axis and scale them to finalize the surface part of the shelf.
![[Screenshot 2024-03-22 at 9.02.47 AM.png|500]]
### Logs

#### Full Logs
- **Create a cylinder for the log.**
- **Apply a bevel to the edges to sharpen them.**

#### Half Logs
- **Use the upside-down mailbox shape from a previous step.**
- **Create a cube, add a loop cut, and then apply a subdivision modifier to it.**
![[Screenshot 2024-03-22 at 9.06.11 AM.png|500]]
#### Duplicate the Logs
- **Position the logs:**
  - Scale and move all the logs into place according to the reference image or design.
![[Screenshot 2024-03-22 at 9.08.43 AM.png|500]]
### Paint Bucket

#### Bucket Creation
- **Forming the bucket:**
  1. Create a cube for the base shape of the bucket.
  2. Add a loop cut at the top and bottom for structure.
  3. Apply a subdivision modifier to smooth the cube.
  4. Use the Inset Faces tool to create the inner part of the bucket.
  5. Extrude downwards to form the bucket's depth.
  6. Apply inset faces again at the bottom to define the base.
![[Screenshot 2024-03-22 at 9.33.04 AM.png|500]]
#### Bucket Edges
- **Shaping the edges:**
  7. Loop select the top edge faces, extrude slightly, then scale to form the lip of the bucket.
  8. Add a loop cut at the bottom edge to sharpen it.
  9. Repeat the same process at the bottom of the bucket.

### Paint
#### Paint Creation
- **Start with a cube to represent the paint inside the bucket.**
![[Screenshot 2024-03-22 at 10.22.38 AM.png|500]]
### Handle Creation

#### Handle for the Bucket
- **Design the handle separately, ensuring it fits with the bucket's dimensions.**
![[Screenshot 2024-03-22 at 1.48.53 PM.png|400]]

### ![[Screenshot 2024-03-22 at 1.57.31 PM.png]]Honey Pot

#### Honey Pot Modeling
- **Create a flattened cube and apply a subdivision surface modifier to smooth it out for the honey pot shape.**
![[Screenshot 2024-03-22 at 4.14.26 PM.png]]

**Honey Pot Cap**
1. Extrude a little to sharpen the edges, inset a little to make sharp edges
![[Screenshot 2024-03-22 at 4.15.55 PM.png|500]]
