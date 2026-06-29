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

淺談Three.js
==

Three.js 是一個開源的 JavaScript 庫，基於 WebGL API 所開發，將 WebGL 上複雜的操作包裝成易上手的 API，方便開發者在網頁瀏覽器中建立 3D 場景、動畫。

探討 Three.js 的發展
==
![](https://i.imgur.com/fqoubAn.png)
 Three.js 是基於 WebGL 發展而來、WebGL 是基於 OpenGL ES 2.0 發展而來、而 OpenGL ES（OpenGL for Embedded Systems） 是 OpenGL 為嵌入式系統特製的版本。

基本上越往 OpenGL 的方向靠近，就會有更多一些底層與硬體加速相關的 API，也會需要了解更多的圖學與數學知識。而 WebGL 可以想成是瀏覽器提供我們 Javascript API 接口，透過這些接口我們可以直接享用 OpenGL 的功能，在瀏覽器上實現強大的 3D 繪圖效果。
![](https://i.imgur.com/MVyjE8w.png)

為甚麼需要Three.js
==
Three.js 最大的優點就是它對 WebGL 進行了良好的封裝，大大的降低了前端工程師們的學習成本，可以說 Three.js 蠻像 3D 網頁中的 jQuery。

另外一點就是 Three.js 具備輕量函式庫的特性，相當適合拿來在 Web 做中小型專案，像是小遊戲或品牌網頁等。
範例：
1. https://threejs.org/examples/
1. http://campoallecomete.it
![](https://i.imgur.com/93u1BSK.jpg)
1. https://threejs.org/examples/#webgl_loader_collada_skinning
1. https://threejs.org/examples/#webgl_shaders_ocean

快速開始
==

1. HTML程式

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

2. 創建場景
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

3. 渲染場景
```javascript=
function animate() {
	requestAnimationFrame( animate );
	renderer.render( scene, camera );
}
animate();
```
5. 為立方體設置動畫
```javascript=
cube.rotation.x += 0.01;
cube.rotation.y += 0.01;
```

7. 結果
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


基本元素
==
* 場景（Scene）：供其他元素設置的空間。
* 相機（Camera）：在場景中建立觀察點，並確定觀察方向、角度。
* 物體（Objects）：在場景中添加被觀察的物體。
* 光源（Light）：在場景中用來照亮物體的光。
* 渲染器（Renderer）：將所要呈現的場景渲染到畫面上。



繪製3D空間的流程
==

1. 建立場景(Scene)
通常使用new THREE.Scene()的方式建立場景

2. 設定相機(Camera)觀察視角、方向
在 Three.js 的世界裡採用右手座標系定位，大拇指代表 X 軸、食指代表 Y 軸、中指為 Z 軸，這三隻手指的指向即為座標軸的正向。
![](https://i.imgur.com/hVFJDjW.png)

而當作觀察點的相機主要分為兩種，透視投影相機 (PerspectiveCamera) 與正交投影相機 (OrthographicCamera)
![](https://i.imgur.com/hZVBHtd.png)

在透視投影相機裡可以看到，物體會隨著視角移動而產生變化，更貼近真實世界的效果，而正交投影相機的物體不論遠近皆沒有差異

3. 添加物體(Objects)到場景中
物體是由 Geometry(幾何體)＋材質 Material(材質) 所組成。
幾何體
就是物體的形狀，從正方形、球體、圓形到各種扭曲體都有
![](https://i.imgur.com/cY5QT30.png)

4. 材質
就是物體的外觀，也記錄除了形狀外的所有可視屬性，如顏色、透明度、紋理、反射率等等

5. 將場景渲染(Renderer)到畫面上
在場景中建立完各種物體後，會創建一個循環，每次刷新時渲染器重新繪製場景，呈現出想要的畫面。

Reference:
https://threejs.org/docs/#api/en/geometries/TubeGeometry



常見材質介紹
==


| 材質 | 說明 |圖示 |
| -------- | -------- | -------- |
MeshBasicMaterial| 網面基礎材質。賦予幾何體一個簡單的顏色，不考慮場景中光源的影響。     | 網面基礎材質。賦予幾何體一個簡單的顏色，不考慮場景中光源的影響。     |![](https://i.imgur.com/8vTMrrV.png)|
| MeshNormalMaterial | 網面法向材質。透過法向量（與面垂直的向量）計算物體表面的顏色，也不受光源影響。 | ![](https://i.imgur.com/GeQSiao.png)
 | MeshLambertMaterial    | 	網面朗伯特材質。受光源影響，常用於創建暗淡不光亮的物體。     | ![](https://i.imgur.com/JTXxuAb.png)|
| MeshPhongMaterial | 網面馮氏材質。受光源影響，常用於創建光亮的物體。 | ![](https://i.imgur.com/jmfkCk4.png)|
| MeshStandardMaterial     | 網面標準材質。基於 PBR（Physically Based Rendering）計算出來的材質，透過更複雜的算法讓物體更能反應在真實物理環境的外觀。     | ![](https://i.imgur.com/6vVaH7Q.png)|

# 材質比較
1. 基礎材質
依據筆者的理解， MeshBasicMaterial 與 MeshNormalMaterial 主要被用在開發過程中的實驗上，由於他們不受光源影響，可以在還沒設置光源到場景中時，使用這兩種材質測試物體是否能正確顯示到畫面中，或是在除錯過程中能排除光源的問題，對材質進行測試。

1. 高級材質
在範例中常會看到 MeshLambertMaterial 與 MeshPhongMaterial，這兩種材質都能與光源有互動，但兩者根據不同的著色算法，會呈現不同的感覺，前者是較黯淡粗糙的塑膠感，後者則是較光亮平滑的金屬感，主要的差異在於馮氏材質具有 鏡面反射（specular） 這個屬性，這個屬性可以指定高光的反射顏色，讓物體更具金屬感。

* 而在查官網文件時，看到兩個相對比較新的材質分別是 MeshStandardMaterial 與 MeshPhysicalMaterial，比起朗伯特與馮氏只是透過近似值來模擬光與材質間的互動，MeshStandardMaterial 使用更複雜的算法，讓物體更具真實感，甚至可以設定金屬感（metalness）與粗糙度（roughness）。

* MeshPhysicalMaterial 則是由前者延伸出來的材質，但多了一個 反射率（reflectivity）的屬性，讓調整的彈性更大。

材質屬性
==

材質屬性	說明
* color	就是材質的顏色
* transparent	是否透明，設為 true 後，可以依據 opacity 調整透明度。
* opacity	透明度，與 transparent 搭配使用，值從 0 到 1。
* wireframe	設為 true 可將材質渲染成線框，適合拿來開發除錯。
* side	決定幾何體哪一面使用此材質，預設為 THREE.FrontSide（外側），另外也可以設定為 THREE.BackSide（內側）、THREE.DoubleSide（兩側）。
* map	貼圖屬性，可透過 THREE.TextureLoader() 載入圖片資源貼在幾何體上。
* 材質的屬性非常之多，這邊只簡單介紹每個材質共用且常見的幾個，更高級的材質還可以設定像是反射率（specular）、亮度（shininess）、材質發散色彩（emissive）等等，建議需要調整細節時再到官網查詢即可！

光源介紹
==
在 Three.js 中有以下幾種基礎光源：
分別有環境光、點光源、聚光燈、平行光



| 光源 | 說明 |
| -------- | -------- | 
| AmbientLight     | 環境光散佈在環境中的光，會將光源的顏色疊加到場景中所有物體上，不能創造陰影，通常拿來增加一些柔性的光線補強色彩。     | 
| PointLight | 點光源。從特定一點向所有方向發射光線，可以投射陰影。類似燈泡、螢火蟲的概念。 |
| SpotLight | 聚光燈。從特定一點對某個方向發射錐形的光線，可以投射陰影。類似手電筒、舞台聚光燈的概念。 | 
| DirectionalLight | 平行光、無限光。從一個二維平面發射光線，光線彼此平行，可以投射陰影，類似太陽光的概念。 | 

以下分別為各種光源的使用方法：

環境光
```javascript=
// 設置環境光 AmbientLight
let ambientLight = new THREE.AmbientLight(0xeeff00)
scene.add(ambientLight)
```

點光源
```javascript=
// 設置點光源 PointLight
let pointLight = new THREE.PointLight(0xeeff00)
pointLight.position.set(-10, 20, 20)
pointLight.castShadow = true
scene.add(pointLight)
let pointLightHelper = new THREE.PointLightHelper(pointLight)
scene.add(pointLightHelper)
```
聚光燈

```javascript=
// 設置聚光燈 SpotLight
let spotLight = new THREE.SpotLight(0xeeff00)
spotLight.position.set(-10, 20, 20)
spotLight.castShadow = true
scene.add(spotLight)
let spotLightHelper = new THREE.SpotLightHelper(spotLight)
scene.add(spotLightHelper)

```
平行光
```javascript=
// 設置平行光 DirectionalLight
let directionalLight = new THREE.DirectionalLight(0xeeff00)
directionalLight.position.set(-10, 20, 20)
directionalLight.castShadow = true
scene.add(directionalLight)
let directionalLightHelper = new THREE.DirectionalLightHelper(
  directionalLight
)
scene.add(directionalLightHelper)
```


延伸閱讀
==

Youtube 教學：
https://youtube.com/playlist?list=PLjcjAqAnHd1EIxV4FSZIiJZvsdrBc1Xho
{{< youtube j7TzxxX1EJk >}}
{{< youtube L12wIvuZTOY >}}
{{< youtube hGIYEBd-NZk >}}
免費3d模型庫：
https://market.pmnd.rs/
React+three.js 參考：
https://docs.pmnd.rs/react-three-fiber/getting-started/introduction