---
title: "CSS3 Canvas"
date: 2018-10-31T18:52:17+08:00
showDate: true
draft: false
tags: ["CSS","Canvas"]
---

Canvas 是 HTML5 新增加的一个元素,它又称为"画布",主要有以下四种功能

- 绘制图形
- 绘制图表
- 动画效果
- 游戏开发

在 chrome 浏览器中,canvas 的默认宽高是 300px 和 150px,写宽高的样式的时候最好写在 HTML 页面的属性值里面

```html
<canvas width="150" height="100" style="border: 1px black dashed"></canvas>
```

一般的操作
<br>1.获取 canvas 对象
<br>2.获取上下文环境对象 context

```js
cxt = canvas.getContext("2d");
```

3.开始绘制图形

## 1.直线

```js
cxt.moveTo(x1,y1)   画笔移到(x1,y1)处
cxt.LineTo(x2,y2)   画笔从起点(x1,y1)开始画线,一直到终点(x2,y2)处
cxt.strokeStyle = "red"     设置线的颜色
cxt.stroke()        用笔划线
(tip:cxt.strokeStyle要在cxt.stroke()之前执行,否则是看不到效果的,和画画是一样的,在动笔之前把要画的东西,颜色,样式确定好
```

## 2.描边矩形 填充矩形 清空矩形

* 描边矩形

```js
cxt.strokeRect(x1,y1,x2,y2)     (x1,y1)为矩形左上角坐标,(x2,y2)为矩形右下角坐标
等价于==>
cxt.rect(x1,y1,x2,y2);
cxt.stroke();
```

* 填充矩形

```js
cxt.fillStyle = "属性值"
cxt.fillRect(x1,y1,width,height) (x1,y1)是矩形左上角坐标,width是矩形的宽度,height是矩形的高度
等价于==>
cxt.rect(x1,y1,x2,y2);
cxt.fill()
```

* 清空矩形

```js
cxt.clearRect(x1, y1, x2, y2);
```

* 绘制一个正 n 多边形

```html
  <canvas width="100" height="50" style="border: 1px black dashed"></canvas>
    <script>
        var canvas = document.getElementsByTagName('canvas')[0]
        var cxt = canvas.getContext('2d');      //获取上下文环境对象
        var cvs_width = parseFloat(getComputedStyle(canvas, null).width);   //获取画布的宽
        var cvs_height = parseFloat(getComputedStyle(canvas, null).height); //获取画布的高
        var distanceR = distanceD = 0 
        function createPolygon(n) {
            var r = Math.min(cvs_width, cvs_height)/2;  //正多边形外接圆半径
            if(Math.min(cvs_width,cvs_height)==cvs_height){
                distanceR = (cvs_width/2) - r
            }else{
                distanceD = (cvs_height/2) - r
            }
            var degree = (2 * Math.PI) / n;     //每个角的度数
            cxt.moveTo(0+distanceR, r+distanceD);   //初始化起点
            for (let i = 1; i < n; i++) {
                cxt.lineTo(r - r * Math.cos(i * degree)+distanceR, r + r * Math.sin(i * degree)+distanceD);
            }
            cxt.closePath();
            cxt.fillStyle = "#f40";
            cxt.fill()
        }
    </script>
```
## 2.曲线
* 圆形

```js
cxt.beginPath() 开始一个路径
cxt.arc(x,y,半径,开始角度,结束角度,anticlockwise)
// (x,y)时圆心的坐标,开始角度和结束角度都是弧度制,anticlockwise(逆时针地)为true时,逆时针绘制图形,为false时,顺时针绘制图形
cxt.closePath() 结束一个路径
// 描边
cxt.strokeStyle = "颜色值" 
cxt.stroke()  画线
// 或者填充
cxt.fillStyle()
cxt.fill()
```
* 弧形

``` js
1.arc() 
// 和画圆基本语法一样,就是把cxt.closePath()去掉就好了
2.arcTo(cx,cy,x2,y2,radius)
// 控制点坐标(cx,cy) 终点坐标(x2,y2) radius是圆弧半径 起点坐标(x1,y1)由一般由moveTo()或lineTo()提供
``` 
* 二次贝塞尔曲线

```js
cxt.quadraticCurveTo(cx,cy,x2,y2)
// (cx,cy)控制点坐标,(x2,y2)终点坐标,起点坐标由moveTo()或lineTo()提供
```
* 三次贝塞尔曲线

```js
cxt.bezierCurveTo(cx1,cy1,cx2,cy2,x,y)
//(cx1,cy1)控制点1的坐标,(cx2,cy2)控制点2的坐标,(x,y)表示结束点坐标,起点坐标由moveTo()或lineTo()提供
```

