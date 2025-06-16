---
created: 2023-09-02 07:11
modified: Saturday 2nd September 2023 07:11:50

---
up::  [[3JS-Three.js Journey]]
tags:: [[react]] [[three.js]]
related:

## Debug

### What is leva?
A GUI component that you can add to your React Three Fiber project to easily interact with your scene.

### Installation and Import

``` javascript
npm install leva@0.9
```

```javascript
import { useControls } from 'leva'
```

Create tweak, we can use `useControls` to create a tweak that lets us change the sphere position and color
```javascript
const sphere = useControls("sphere", {
	color: "#ff0000",
	position: {
		value: [1, 1, 0],
		step: 0.1,
		joystick: "invertY",
	},
	scale: {
		value: 1.5,
		min: -4,
		max: 4,
		step: 0.01,
	},
});
```

Apply the properties to the sphere mesh
``` javascript
<mesh
	ref={spehereRef}
	position={sphere.position}
	scale={sphere.scale}>
<sphereGeometry />
<meshBasicMaterial color={sphere.color} />
</mesh>
```

### Button, Select and Intervals
We can create buttons on our debug GUI controls that will call a function once clicked.
We can use this button to play an animation, fetch data, changes some values.
![[Screenshot 2023-09-02 at 11.02.58 AM.png]]

```javascript
import { button, useControls } from 'leva'
```

```javascript
const sphere = useControls('sphere', {
	  // ...
	  clickMe: button(() => { console.log('ok') }),
	  choice: { options: ['a', 'b', 'c']},
	  myInterval:
	    {
	        min: 0,
	        max: 10,
	        value: [4, 5],
	    }
})
```
