---
created: 2023-08-29 06:41
modified: Tuesday 29th August 2023 06:43:39
alias:
---
up::  [[Three.js Journey]]
tags:: #threejs
source:

## three.js.cameras

### Cameras

### Perspective Camera
```javascript
const camera = new THREE.PerspectiveCamera( 45, width / height, 1, 1000 ); scene.add( camera );
```
```javascript
PerspectiveCamera( fov : Number, aspect : Number, near : Number, far : Number )
```
**Field of View (FOV)**:`45` and `75` are good values to use
	Small value: long scope effect
	Large value: fish eye effect, what is camera sees will be stretched
	Minecraft FOV
**Aspect ratio**:
```javascript
const sizes = {
    width: 800,
    height: 600
}
```
width divided by the height

**Near and far**
These parameters correspond to how close and how far the camera can see.
We often see this is old racing games, where you can see trees pop up in the distance an more forward
### Controls
[OrbitControls – three.js docs](https://threejs.org/docs/index.html#examples/en/controls/OrbitControls)
	Orbit controls allow the camera to orbit around a target.
### Code
```javascript
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'

/**
 * Base
 */
// Canvas
const canvas = document.querySelector('canvas.webgl')

// Sizes
const sizes = {
    width: 800,
    height: 600
}

// Cursor
const cursor = {
    x: 0,
    y: 0
}

window.addEventListener('mousemove', (event) =>
{
    cursor.x = event.clientX / sizes.width - 0.5
    cursor.y = - (event.clientY / sizes.height - 0.5)
})

// Scene
const scene = new THREE.Scene()

// Object
const mesh = new THREE.Mesh(
    new THREE.BoxGeometry(1, 1, 1, 5, 5, 5),
    new THREE.MeshBasicMaterial({ color: 0xff0000 })
)
scene.add(mesh)

// Camera
const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height, 0.1, 100)
// const aspectRatio = sizes.width / sizes.height
// const camera = new THREE.OrthographicCamera(- 1 * aspectRatio, 1 * aspectRatio, 1, - 1, 0.1, 100)
camera.position.z = 3
scene.add(camera)

// Controls
const controls = new OrbitControls(camera, canvas)
controls.enableDamping = true

// Renderer
const renderer = new THREE.WebGLRenderer({
    canvas: canvas
})
renderer.setSize(sizes.width, sizes.height)

// Animate
const clock = new THREE.Clock()

const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()

    // Update controls
    controls.update()

    // Render
    renderer.render(scene, camera)

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}

tick()
```
