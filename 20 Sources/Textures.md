---
created: 2023-08-30 11:26
modified: 2025-06-15T20:27:08-04:00

---
up::
related:

## three.js.textures

Textures are images that cover the surface of geometries

### Types of textures
1. **Color**: takes the pixels of the texture and applies them to the geometry
2. **Alpha**: grayscale image where white is visible and black is not
3. **Normal**: adds small details without subdividing the geometry
	- Creates convincing fake the lighting of bumps, scratches and dents on a low-polygon model surface at very low computational costs compared to displacement mapping or high poly meshes
1. **Ambient** occlusion: creates fake shadows in the surface crevices.
2. **Metalness**: creates reflection, specifies which part is metallic (white) and not metallic (black)
3. **Roughness**: rough (white) and smooth (black). Comes with metalness and disspates light. A carpet is rugged, so you will not see any light reflection, while water is smooth, and you can see light reflecting on it.
4. **Displacement Map**: used to add detail and **depth** to 3D models and textures, Grayscale image that stores height information. **Brighter** values represent **higher areas**, darker **values** are **lower areas.**Moves vertices in the mesh based on a displacement map image. In contrast to normal maps, displacements maps subdivides and modifies the actual geometry of them mesh.
	**How are they used and their purpose?**
	- Common uses are adding texture like **cracks** or wrinkles to skin or cloth, **bumps** and **dents** to surfaces like stone or metal, deforming an initially flat surface to add relief and depth.
	- Displacement mapping can **simulate detail that would be too complex to model directly in the mesh**. It's a more efficient way to add complexity than simply increasing the polygon count.

### Loading Manager
```javascript
const loadingManager = new THREE.LoadingManager()
loadingManager.onStart = () =>
{
    console.log('loading started')
}
loadingManager.onLoad = () =>
{
    console.log('loading finished')
}
loadingManager.onProgress = () =>
{
    console.log('loading progressing')
}
loadingManager.onError = () =>
{
    console.log('loading error')
}

const textureLoader = new THREE.TextureLoader(loadingManager)
```
The [LoadingManager](https://threejs.org/docs/index.html#api/en/loaders/managers/LoadingManager) is very useful if you want to show a loader and hide it only when all the assets are loaded.
Start loading the images
### Loading Multiple Textures
```javascript
const textureLoader = new THREE.TextureLoader();

const doorColortexture = textureLoader.load(
    '/textures/door/color.jpg',
    () =>
    {
        console.log('loading finished')
    },
    () =>
    {
        console.log('loading progressing')
    },
    () =>
    {
        console.log('loading error')
    }
)
const doorAlphaTexture = textureLoader.load("/textures/door/alpha.jpg");
const doorAmbientOcclusionTexture = textureLoader.load(
  "/textures/door/ambientOcclusion.jpg"
);
const doorHeightTexture = textureLoader.load("/textures/door/height.jpg");
const doorNormalTexture = textureLoader.load("/textures/door/normal.jpg");
const doorMetalnessTexture = textureLoader.load("/textures/door/metalness.jpg");
const doorRoughnessTexture = textureLoader.load("/textures/door/roughness.jpg");

```

### Apply the textures
```javascript
// Door
const door = new THREE.Mesh(
  new THREE.PlaneGeometry(2, 2),
  new THREE.MeshStandardMaterial({
    map: doorColorTexture,
    transparent: true,
    alphaMap: doorAlphaTexture,
    aoMap: doorAmbientOcclusionTexture,
    displacementMap: doorHeightTexture,
    displacementScale: 0.1,
    normalMap: doorNormalTexture,
    metalnessMap: doorMetalnessTexture,
    roughnessMap: doorRoughnessTexture,
  })
);
```

### Repeat Mapping
``` javascript
// Grass textures
const grassColorTexture = textureLoader.load("/textures/grass/color.jpg");

// In order to activate the repeat we need to change the wrpS and wrapT properties of the textures
//This defines how the {@link Texture} is wrapped *horizontally* and corresponds to **U** in UV mapping.
grassColorTexture.wrapS = THREE.RepeatWrapping;
//This defines how the {@link Texture} is wrapped *vertically* and corresponds to **V** in UV mapping.
grassColorTexture.wrapT = THREE.RepeatWrapping;

// since the texture is too large we can repeat each grass texture 8 times with the repeat property
// How many times the texture is repeated across the surface, in each direction **U** and **V**.
grassColorTexture.repeat.set(8, 8);

const floor = new THREE.Mesh(
  new THREE.PlaneGeometry(20, 20),
  new THREE.MeshStandardMaterial({
    map: grassColorTexture,
    aoMap: grassAmbientOcclusionTexture,
    normalMap: grassNormalTexture,
    roughnessMap: grassRoughnessTexture,
  })
);
```

### Filter and Mipmapping

### Minification filter
The texture is too big for the surface, it covers.


## Magnification filter
The texture too small for the surface it covers.
