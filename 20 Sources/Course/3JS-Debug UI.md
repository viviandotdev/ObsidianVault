---
modified: 2025-06-13T08:16:04-04:00
---
up::  [[3JS-Three.js Journey]]
tags:: 
related: 

## three.js.lil-gui

lil-GUI is a three.js debug UI that makes it easy to debug and tweak your code.

### Install
1. `npm install --save lil-gui`
2. Import lil-gui
	```javascript
import './style.css'
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
import gsap from 'gsap'
import * as dat from 'lil-gui'
```
3. instantiate
	```javascript
/**
 * Debug
 */
const gui = new dat.GUI()
```
4. Add elements (the first parameter is the object and the parameter element is the property of the object you would like to tweak)
		`gui.add(mesh.position, 'y')`
5. You can also add and trigger your own functions, first add the function to the object. We can trigger the function with the gui  `gui.add(parameters, 'spin')`
```javascript
const parameters = {
    color: 0xff0000,
    spin: () =>
    {
        gsap.to(mesh.rotation, { duration: 1, y: mesh.rotation.y + Math.PI * 2 })
    }
}

/**
 * Debug
 */

const gui = new dat.GUI()
gui.add(mesh.position, 'y')
gui
    .add(mesh.position, 'y')
    .min(- 3)
    .max(3)
    .step(0.01)
    .name('elevation')

gui.add(mesh, 'visible')
gui.add(material, 'wireframe')
gui
    .addColor(parameters, 'color')
gui.add(parameters, 'spin')

```
### 
### Resources
[lil-gui 0.18.2](https://lil-gui.georgealways.com/)
[Bruno Simon](https://bruno-simon.com/#debug)