---
title: "Three.js"
date: 2018-11-16T23:43:52+08:00
showDate: true
draft: false
tags: ["THREE","three","three.js","3D"]
---
## 1.scene 场景
scene就是一个可以放置物体、灯光的3D空间，和现实中的一个空间相似，可大可小
```js
//创建一个场景
var scene = new THREE.Scene();
```
## 2.camera 相机
camera决定看一个物体的方式和位置，和现实中的相机行为相似，有很多种类的相机。

### * PerspectiveCamera 透视相机
透视相机更加接近于现实中我们看物体的视角，远小近大
```js
// 创建一个透视相机
var camera = new THREE.PerspectiveCamera(fov可视角度,aspect纵横比,near近端距离,far远端距离)
// 设置camera的位置
camera.set(x,y,z)
```
<img src="/PCamera.jpg">
## 3.渲染器
* WebGLRenderer

```js
var renderer = new THREE.WebGLRenderer()
```


## 4.物体

* Mesh 构造器

```js
// 基于以三角形为polygon mesh多边形网格的物体的类
Mesh(geometry:Geometry,material:Material)
```

## 5，加载器
* ImageLoader

```js
// 初始化一个加载器
var loader = new THREE.ImageLoader();
// 加载一个图片资源
loader.load(
    // 资源URL
    './image/1.jpg',
    // onLoad回调
    function(image){ 
        var canvas = document.createElement('canvas');
        var context = canvas.getContext('2d');
        context.drawImage(image,100,100)
    }
)
```













```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>使用three.js创建一个球</title>
    </head>
    <body>
        <script type="text/javascript" src="three.js"></script>
        <script type="text/javascript" src="OrbitControls.js"></script>
        <script type="text/javascript">
            // 创建一个场景
            var scene = new THREE.Scene();
            // 创建一个透视视图相机
            var camera = new THREE.PerspectiveCamera(45,window.innerWidth/innerHeight,1,1000);
            // 设置相机的位置(x,y,z)
            camera.position.set(0,0,5);
            // 创建一个渲染器
            var renderer = new THREE.WebGLRenderer();
            // 设置渲染器的大小
            renderer.setSize(window.innerWidth,window.innerHeight);
            // 设置背景颜色
            renderer.setClearColor(0xfff6e6)
            // 插入到页面当中
            document.body.appendChild(renderer.domElement);

            // 开始渲染(表演开始....)
            // 创建一个球使用SphereGeometry()
            var geomery = new THREE.SphereGeometry(1,22,22);
            // 选择材料
            var material = new THREE.MeshNormalMaterial({wireframe:true});
            // 创建网格对象
            var sphere = new THREE.Mesh(geomery, material);
            // 加入到场景(舞台)当中
            scene.add(sphere);
            // 创建一个控制器
            var controls = new THREE.OrbitControls(camera,renderer.domElement);
            controls.addEventListener('change',function(){
                renderer.render(scene,camera)
            })
            // 渲染
            renderer.render(scene,camera)
            // var animation = function(){
            //     requestAnimationFrame(animation);
            //     sphere.rotation.x += 0.01;
            //     sphere.rotation.y += 0.01;
            //     renderer.render(scene,camera)
            // }
            // animation()
        </script>
    </body>
</html>
```
