---
slug: Three-js
title: Three.js
date: 2025-10-28 12:21:08
tags:
- js
- three.js

categories:
  - Note
---
slug: Three-js

A Brief Introduction to Three.js
==

Three.js is an open-source JavaScript library built on top of the WebGL API. It wraps the complex operations of WebGL into easy-to-use APIs, making it convenient for developers to create 3D scenes and animations in web browsers.

Exploring the Development of Three.js
==
![](https://i.imgur.com/fqoubAn.png)
 Three.js is built on top of WebGL, WebGL is built on top of OpenGL ES 2.0, and OpenGL ES (OpenGL for Embedded Systems) is a version of OpenGL specifically tailored for embedded systems.

Generally speaking, the closer you get to OpenGL, the more low-level and hardware-acceleration-related APIs there are, and the more knowledge of computer graphics and mathematics is required. WebGL can be thought of as a JavaScript API interface provided by browsers that allows us to directly leverage OpenGL's capabilities to achieve powerful 3D graphics effects in the browser.
![](https://i.imgur.com/MVyjE8w.png)

Why Do We Need Three.js
==
Three.js's greatest advantage is its excellent encapsulation of WebGL, which greatly reduces the learning curve for front-end developers. You could say Three.js is like the jQuery of 3D web development.

Another point is that Three.js has the characteristics of a lightweight library, making it very suitable for small-to-medium scale web projects such as small games or brand websites.
Examples:
1. https://threejs.org/examples/
1. http://campoallecomete.it
![](https://i.imgur.com/93u1BSK.jpg)
1. https://threejs.org/examples/#webgl_loader_collada_skinning
1. https://threejs.org/examples/#webgl_shaders_ocean

Quick Start
==

1. HTML Program

```html=
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>My first three.js app</title>
		<style>
			body { margin: 0; }
		</style>
	</head>
	<body>
		<script type="module">
			import * as THREE from 'https://unpkg.com/three/build/three.module.js';

			// Our Javascript will go here.
		</script>
	</body>
</html>
```

2. Create a Scene
```javascript=
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

const renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );

const geometry = new THREE.BoxGeometry( 1, 1, 1 );
const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
const cube = new THREE.Mesh( geometry, material );
scene.add( cube );

camera.position.z = 5;
```

3. Render the Scene
```javascript=
function animate() {
	requestAnimationFrame( animate );
	renderer.render( scene, camera );
}
animate();
```
5. Animate the Cube
```javascript=
cube.rotation.x += 0.01;
cube.rotation.y += 0.01;
```

7. Final Result
```html=
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>My first three.js app</title>
		<style>
			body { margin: 0; }
		</style>
	</head>
	<body>
		<script type="module">
			import * as THREE from 'https://unpkg.com/three/build/three.module.js';

			const scene = new THREE.Scene();
			const camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 );

			const renderer = new THREE.WebGLRenderer();
			renderer.setSize( window.innerWidth, window.innerHeight );
			document.body.appendChild( renderer.domElement );

			const geometry = new THREE.BoxGeometry( 1, 1, 1 );
			const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
			const cube = new THREE.Mesh( geometry, material );
			scene.add( cube );

			camera.position.z = 5;

			function animate() {
				requestAnimationFrame( animate );

				cube.rotation.x += 0.01;
				cube.rotation.y += 0.01;

				renderer.render( scene, camera );
			}

			animate();
		</script>
	</body>
</html>

```


Basic Elements
==
* Scene: The space in which other elements are placed.
* Camera: Establishes a viewpoint in the scene and determines the direction and angle of observation.
* Objects: The objects being observed that are added to the scene.
* Light: Light sources used to illuminate objects in the scene.
* Renderer: Renders the scene to be displayed onto the screen.



The 3D Space Drawing Workflow
==

1. Create a Scene
Usually created using `new THREE.Scene()`

2. Configure the Camera (viewpoint and direction)
Three.js uses a right-hand coordinate system: the thumb represents the X axis, the index finger represents the Y axis, and the middle finger represents the Z axis - the direction these fingers point is the positive direction of each axis.
![](https://i.imgur.com/hVFJDjW.png)

The cameras used as viewpoints are mainly two types: PerspectiveCamera and OrthographicCamera.
![](https://i.imgur.com/hZVBHtd.png)

In a perspective camera, objects change as the viewing angle moves, more closely mimicking the real world, while in an orthographic camera objects look the same regardless of distance.

3. Add Objects to the Scene
Objects are composed of Geometry + Material.
Geometry
This is the shape of the object - from cubes, spheres, and circles to various twisted forms.
![](https://i.imgur.com/cY5QT30.png)

4. Material
This is the appearance of the object, and records all visible properties beyond shape, such as color, transparency, texture, reflectivity, etc.

5. Render the Scene to the Screen
After all objects are set up in the scene, a loop is created where the renderer redraws the scene on every refresh to display the desired view.

Reference:
https://threejs.org/docs/#api/en/geometries/TubeGeometry



Common Materials Overview
==


| Material | Description | Preview |
| -------- | -------- | -------- |
MeshBasicMaterial| Basic mesh material. Gives a geometry a simple color without considering the influence of light sources in the scene. | Basic mesh material. Gives a geometry a simple color without considering the influence of light sources in the scene. |![](https://i.imgur.com/8vTMrrV.png)|
| MeshNormalMaterial | Normal mesh material. Calculates the color of the object's surface using normal vectors (vectors perpendicular to the surface), also unaffected by light sources. | ![](https://i.imgur.com/GeQSiao.png)
 | MeshLambertMaterial | Lambert mesh material. Affected by light sources, commonly used to create dull, non-shiny objects. | ![](https://i.imgur.com/JTXxuAb.png)|
| MeshPhongMaterial | Phong mesh material. Affected by light sources, commonly used to create shiny objects. | ![](https://i.imgur.com/jmfkCk4.png)|
| MeshStandardMaterial | Standard mesh material. A PBR (Physically Based Rendering) material calculated using a more complex algorithm to make objects better reflect their appearance in a real physical environment. | ![](https://i.imgur.com/6vVaH7Q.png)|

# Material Comparison
1. Basic Materials
From the author's understanding, MeshBasicMaterial and MeshNormalMaterial are primarily used during development for experimentation. Since they are unaffected by light sources, they can be used to test whether objects display correctly on screen before light sources have been added to the scene, and can also help isolate lighting issues during debugging.

1. Advanced Materials
You will often see MeshLambertMaterial and MeshPhongMaterial in examples. Both materials interact with light sources, but due to different shading algorithms they produce different looks: the former has a dull, rough plastic feel, while the latter has a shinier, smoother metallic feel. The main difference is that Phong material has a specular property that can specify the highlight reflection color, giving objects a more metallic appearance.

* When checking the official documentation, two relatively newer materials were found: MeshStandardMaterial and MeshPhysicalMaterial. Unlike Lambert and Phong which only use approximations to simulate the interaction between light and material, MeshStandardMaterial uses a more complex algorithm to make objects look more realistic, and can even set metalness and roughness.

* MeshPhysicalMaterial is an extension of the former, but adds a reflectivity property for greater adjustment flexibility.

Material Properties
==

Material Property - Description
* color - The color of the material.
* transparent - Whether the material is transparent; set to true to enable transparency adjustment via opacity.
* opacity - Transparency level, used together with transparent, ranges from 0 to 1.
* wireframe - Set to true to render the material as a wireframe, useful for development and debugging.
* side - Determines which side of a geometry uses this material; default is THREE.FrontSide (outer side), can also be set to THREE.BackSide (inner side) or THREE.DoubleSide (both sides).
* map - Texture property; an image resource can be loaded via THREE.TextureLoader() and applied to the geometry.
* There are many more material properties; this section only briefly introduces a few common ones shared by all materials. More advanced materials can also set properties such as specular, shininess, emissive color, etc. - it is recommended to check the official documentation when you need to fine-tune details.

Light Sources Overview
==
Three.js has the following basic light sources:
AmbientLight, PointLight, SpotLight, and DirectionalLight.



| Light Source | Description |
| -------- | -------- | 
| AmbientLight | Ambient light distributed throughout the environment. It adds the light source color to all objects in the scene, cannot cast shadows, and is typically used to add some soft fill light to enhance color. |
| PointLight | Point light. Emits light rays in all directions from a specific point, can cast shadows. Similar to the concept of a light bulb or a firefly. |
| SpotLight | Spotlight. Emits a cone of light in a specific direction from a specific point, can cast shadows. Similar to the concept of a flashlight or stage spotlight. |
| DirectionalLight | Directional light, also called infinite light. Emits parallel light rays from a two-dimensional plane, rays are parallel to each other, can cast shadows. Similar to the concept of sunlight. |

The following are the usage methods for each light source:

Ambient Light
```javascript=
// Set up AmbientLight
let ambientLight = new THREE.AmbientLight(0xeeff00)
scene.add(ambientLight)
```

Point Light
```javascript=
// Set up PointLight
let pointLight = new THREE.PointLight(0xeeff00)
pointLight.position.set(-10, 20, 20)
pointLight.castShadow = true
scene.add(pointLight)
let pointLightHelper = new THREE.PointLightHelper(pointLight)
scene.add(pointLightHelper)
```
Spotlight

```javascript=
// Set up SpotLight
let spotLight = new THREE.SpotLight(0xeeff00)
spotLight.position.set(-10, 20, 20)
spotLight.castShadow = true
scene.add(spotLight)
let spotLightHelper = new THREE.SpotLightHelper(spotLight)
scene.add(spotLightHelper)

```
Directional Light
```javascript=
// Set up DirectionalLight
let directionalLight = new THREE.DirectionalLight(0xeeff00)
directionalLight.position.set(-10, 20, 20)
directionalLight.castShadow = true
scene.add(directionalLight)
let directionalLightHelper = new THREE.DirectionalLightHelper(
  directionalLight
)
scene.add(directionalLightHelper)
```


Further Reading
==

YouTube Tutorials:
https://youtube.com/playlist?list=PLjcjAqAnHd1EIxV4FSZIiJZvsdrBc1Xho
{{< youtube j7TzxxX1EJk >}}
{{< youtube L12wIvuZTOY >}}
{{< youtube hGIYEBd-NZk >}}
Free 3D Model Library:
https://market.pmnd.rs/
React + Three.js Reference:
https://docs.pmnd.rs/react-three-fiber/getting-started/introduction
