---
created: 2023-08-29 06:41
modified: 2025-06-16T08:05:25-04:00
---
up:: [[3JS-Three.js Journey]]
source: [Three.js Journey — Transform objects](https://threejs-journey.com/lessons/transform-objects)

## Transform Objects

### Transforms
There are 4 properties to transform objects in our scene
- `position` (to move the object)
- `scale` (to resize the object)
- `rotation` (to rotate the object)
- `quaternion` (to also rotate the object; more about that later)

- The `position` possesses 3 essential properties, which are `x`, `y`, and `z`. In Three.js, we usually consider that the `y` axis is going upward, the `z` axis is going backward, and the `x` axis is going to the right.
### [AxesHelper](https://threejs.org/docs/#api/en/helpers/AxesHelper)
The [AxesHelper](https://threejs.org/docs/#api/en/helpers/AxesHelper) will display 3 lines corresponding to the `x`, `y` and `z` axes, each one starting at the center of the scene and going in the corresponding direction.
```javascript
/**
 * Axes Helper
 */
const axesHelper = new THREE.AxesHelper(2)
scene.add(axesHelper)
```
### Scale
- `scale` is also a [Vector3](https://threejs.org/docs/#api/en/math/Vector3). By default, `x`, `y` and `z` are equal to `1`, meaning that the object has no scaling applied. If you put `0.5` as a value, the object will be half of its size on this axis, and if you put `2` as a value, it will be twice its original size on this axis. Clearly, we cannot see the `z` scale because our [Mesh](https://threejs.org/docs/#api/en/objects/Mesh) is facing the camera.
![[Screenshot 2023-08-29 at 6.47.35 AM.png]]
```javascript
// Object
const geometry = new THREE.BoxGeometry(1, 1, 1)
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 })
const mesh = new THREE.Mesh(geometry, material)

mesh.scale.x = 2
mesh.scale.y = 0.25
mesh.scale.z = 0.5
```
### Rotation
- `rotation` ([Euler](https://threejs.org/docs/index.html#api/en/math/Euler)) property has `x`, `y`, `z` properties.
	- When changing the  `x`, `y`, `z` properties imagine putting a stick through the object's center in the axis's direction and rotating that object on that stick
- when you rotate on the `y` axis imagine a carousel
- when you rotate on the `x` axis imagine rotating the wheels of a car
- when you rotate on the `z` axis imagine rotating propellers in the front of an aircraft you are in


```javascript
// Object
const geometry = new THREE.BoxGeometry(1, 1, 1)
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 })
const mesh = new THREE.Mesh(geometry, material)

mesh.rotation.x = Math.PI * 0.25
mesh.rotation.y = Math.PI * 0.25

```


### Scene graph
At some point, you might want to group things. Let's say you are building a house with walls, doors, windows, a roof, bushes, etc.
You can do that with the [Group](https://threejs.org/docs/#api/en/objects/Group) class.


````javascript
/**
 * Objects
 */
const group = new THREE.Group()
group.scale.y = 2
group.rotation.y = 0.2
scene.add(group)

const cube1 = new THREE.Mesh(
    new THREE.BoxGeometry(1, 1, 1),
    new THREE.MeshBasicMaterial({ color: 0xff0000 })
)
cube1.position.x = - 1.5
group.add(cube1)

const cube2 = new THREE.Mesh(
    new THREE.BoxGeometry(1, 1, 1),
    new THREE.MeshBasicMaterial({ color: 0xff0000 })
)
cube2.position.x = 0
group.add(cube2)

const cube3 = new THREE.Mesh(
    new THREE.BoxGeometry(1, 1, 1),
    new THREE.MeshBasicMaterial({ color: 0xff0000 })
)
cube3.position.x = 1.5
group.add(cube3)
````
