---
created: 2023-08-30 12:00
modified: 2025-06-15T20:47:57-04:00

---
up::  [[3JS-Three.js Journey]]
related:
## Materials

**Table of Contents**
- [[#MeshBasicMaterial|MeshBasicMaterial]]
- [[#MeshNormalMaterial|MeshNormalMaterial]]

### MeshBasicMaterial
[MeshBasicMaterial](https://threejs.org/docs/#api/en/materials/MeshBasicMaterial) is probably the most "basic" material... But there are multiple properties that we haven't covered yet.
Create 3 meshes of 3 different geometries and apply the same material to all 3

```javascript
 /**
 * Objects
 */
const material = new THREE.MeshBasicMaterial({map : doorColorTexture})

const sphere = new THREE.Mesh(
    new THREE.SphereGeometry(0.5, 16, 16),
    material
)
sphere.position.x = - 1.5

const plane = new THREE.Mesh(
    new THREE.PlaneGeometry(1, 1),
    material
)

const torus = new THREE.Mesh(
    new THREE.TorusGeometry(0.3, 0.2, 16, 32),
    material
)
torus.position.x = 1.5

scene.add(sphere, plane, torus)
```

To map textures on to your material we can use a the `map` property. Combining `color` and `map` will tint the texture with the color:

```javascript
material.map = doorColorTexture
material.color = new THREE.Color('#ff0000')
```

The `wireframe` property will show the triangles that compose your geometry with a thin line of 1px regardless of the distance of the camera:
```javascript
material.wireframe = true
```
The `opacity` property controls the transparency but, to work, you should set the `transparent` property to `true` to inform Three.js that this material now supports transparency:
```javascript
material.transparent = true
material.opacity = 0.5
```


### MeshNormalMaterial
The [MeshNormalMaterial](https://threejs.org/docs/#api/en/materials/MeshNormalMaterial) displays a nice purple, blueish, greenish color that looks like the normal texture we saw in the Textures lessons.

Normals are information encoded in each vertex that contains the direction of the outside of the face. They are used to for calculating how to illuminate the face or how the environment should rreflector refract on the geometries' surface.
```javascript
const material = new THREE.MeshNormalMaterial()
```
