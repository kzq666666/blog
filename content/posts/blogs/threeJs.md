---
title: "Three.js"
date: 2018-11-16T23:43:52+08:00
showDate: true
draft: false
tags: ["THREE","three","three.js","3D"]
---
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>使用three.js创建一个球</title>
    </head>
    <body>
        <script type="text/javascript" src="three.js"></script>
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
            scene.add(sphere)
            // 渲染
            var animation = function(){
                requestAnimationFrame(animation);
                sphere.rotation.x += 0.01;
                sphere.rotation.y += 0.01;
                renderer.render(scene,camera)
            }
            animation()
        </script>
    </body>
</html>
```
