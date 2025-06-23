---
created: 2023-09-07 07:15
modified: Thursday 7th September 2023 08:59:59

---
up::  [[+ 3JS-Three.js Journey]]
tags::
source: [Three.js Journey — Scroll based animation](https://threejs-journey.com/lessons/scroll-based-animation#easing)

## Threejs Journey-Scroll based animation

### Animate meshes
**Notes on high frequency displays**
- tick function in Three.js is called every frame to update animations, physics, input, etc. It is tied to the browser's requestAnimationFrame.
- On higher frequency displays (120Hz, 144Hz, etc), requestAnimationFrame will fire more often, so Three.js's tick function will be called more times per second.
- This means animations and physics simulations will update more frequently on high refresh rate displays

```javascript

const clock = new THREE.Clock()
let previousTime = 0 //keeps track of the previous time to get the change in time

const tick = () => // tick () is called on each tick or frame of the scene's render loop.
{
  const elapsedTime = clock.getElapsedTime();
  //Get the seconds passed since the clock started
  const deltaTime = elapsedTime - previousTime //get the chanage it time for each tick
  previousTime = elapsedTime

  // Animate meshes
    for(const mesh of sectionMeshes)
    {
        mesh.rotation.x += deltaTime * 0.1
        mesh.rotation.y += deltaTime * 0.12
    }
}
```


### Parallax uses CSS and JavaScript to make the background sections move slower than the foreground, creating an illusion of 3D depth as you scroll.
-
Put the camera in a group, because we are updating the camera position twice once on the on scroll and then again for the parallax effect
```javascript
/**
 * Camera
 */
// Group
const cameraGroup = new THREE.Group()
scene.add(cameraGroup)

// Base camera
const camera = new THREE.PerspectiveCamera(35, sizes.width / sizes.height, 0.1, 100)
camera.position.z = 6
cameraGroup.add(camera)
```

#### Easing
 We are going to add some "easing" (also called "smoothing" or "lerping") and we are going to use a well-known formula. The idea behind the formula is that, on each frame, instead of moving the camera straight to the target, we are going to move it (let's say) a 10th closer to the destination. Then, on the next frame, another 10th closer. Then, on the next frame, another 10th closer. The closer it gets, the slower it moves because it's always a 10th of the actual position toward the target position, and it will never reach the destination
 -Use that `deltaTime` on the parallax, but, because the `deltaTime` is in seconds, the value will be very small (around `0.016` for most common screens running at 60fps). Consequently, the effect will be very slow even on high frequency displays.
 
```javascript
const tick = () =>
{
    // ...
    // Animate camera
    camera.position.y = - scrollY / sizes.height * objectsDistance

    const parallaxX = cursor.x * 0.5
    const parallaxY = - cursor.y * 0.5

	cameraGroup.position.x += (parallaxX - cameraGroup.position.x) * 5 * deltaTime
    cameraGroup.position.y += (parallaxY - cameraGroup.position.y) * 5 * deltaTime

    // ...
}
```


### Animate mesh when detect section changed

```javascript
let scrollY = window.scrollY
let currentSection = 0
```


```javascript
window.addEventListener('scroll', () =>
{
    scrollY = window.scrollY
    const newSection = Math.round(scrollY / sizes.height)

    if(newSection != currentSection)
    {
        currentSection = newSection
        gsap.to(
            sectionMeshes[currentSection].rotation,
            {
                duration: 1.5,
                ease: 'power2.inOut',
                x: '+=6',
                y: '+=3'
            }
        )
    }
})
```
