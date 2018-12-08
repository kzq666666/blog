---
title: "Q && A"
date: 2018-11-16T10:01:19+08:00
showDate: true
draft: false
tags: ["Question"]
---

 
## 1. return !1 和 return false 以及 return 0! 和 return true写法有什么区别
```js
tween.min.js的源码
update: function(c) {
        if (0 === a.length) return !1;
        for (
          var b = 0, d = a.length, c = void 0 !== c ? c : Date.now();
          b < d;

        )
          a[b].update(c) ? b++ : (a.splice(b, 1), d--);
        return !0;
      }
```

## 2. void 和 undefined 有什么区别(详细请看[这里](https://segmentfault.com/a/1190000000474941))
A : void是一种操作符,无论void后的表达式是什么，void操作符都会返回undefined.但undefined不是[`保留字`](https://baike.baidu.com/item/%E4%BF%9D%E7%95%99%E5%AD%97),undefined可以作为变量使用,所以在使用undefined作为变量名的时候容易出错,因此使用void可以确保取到undefined值
```js
function x() {
   var undefined = 'hello world',
       f = {},
       window = {
           'undefined': 'joke'
       };
   console.log(undefined);// hello world
   console.log(window.undefined); //joke
   console.log(f.a === undefined); //false
   console.log(f.a === void 0); //true
}
```
* void还有一个经常使用到的作用,就是在a标签的href中使用,填充href,使它不跳转而是进行一些交互,比如在许多网站中的收藏,快转功能.

``` html
<a href="javascript:void(0)">
```

* 生成一个空的src的img标签的最好的方式似乎是使用`src="javascript:void(0)"`
<br>详情请看[What's the valid way to include an image with no src?](https://stackoverflow.com/questions/5775469/whats-the-valid-way-to-include-an-image-with-no-src)

<br> Tip : 关于此问题更加详细请看[这里](https://segmentfault.com/a/1190000000474941)

## 3.null!=a 和 a!=null的区别
## 4.常见的获取元素宽高的方式及其区别
* dom.style.width/height 
  <br>这种方式只能获取dom元素`内联样式`的宽高，而style标签的样式和外联样式使获取不到的。修改样式用这个还是可以的
* dom.currentStyle.width/height 
  <br>无论哪种样式都可以获得，不过只有IE浏览器支持(我亲测了chrome和firefox都是不兼容的)。只读
* window.getComputedStyle(element,[preudoElt]).width/height
  <br>首先getComputedStyle(element,[preudoElt])返回的是一个实时的css属性对象preudoElt是伪元素(可选),对于普通元素就是设置为null即可。兼容性更好(IE、firefox、chrome都可以)。只读
* dom.offsetWidth/offsetHeight 
  <br>兼容性很好，常用，且返回值是数字，不带单位。只读
* dom.getBoundingClientRect().width/height
  <br>getBoundingClientRect()返回的是一个元素的绝对位置的DomRect对象，里面有top、bottom、left、right、width、height,IE不兼容getBoundingClientRect(),IE兼容getClientRects(),其他浏览器都兼容，返回值是数值，不带单位。只读

<br>以上，个人觉得offsetWidth比较方便一些
## 5.window.onload和$(document).ready()方法的区别
A：window.onload事件会在页面所有元素加载完成后立即发生。而$(document).ready()是在DOM树加载完毕之后对其进行操作