---
title: "ES6"
date: 2019-01-04T11:03:38+08:00
showDate: true
draft: false
tags: ["ES6"]
---
## let 和 const
ES6新加了两种声明变量的方式，一个是let，一个是const。

* let和const声明变量有自己的块级作用域（在for循环中用let声明的变量不会泄露到外部）
* let和const声明变量在预编译的过程都不会进行变量提升
* let和const声明的变量不能再次声明，而const声明变量的时候必须同时赋值，并且不能再次赋值

```js
{
    console.log(a); // ReferenceError:a is not undefined
    let a;
}
{
    let a = 1;
    let a = 2; // SyntaxError: Identifier 'a' has already been declared
}
{
    const a; // SyntaxError:Missing initializer in const declaration
}

{
    const a = 1;
    a = 2 // TypeError:Assignment to constant variable
}
```
## 模板字面量
* 创建字符串不必再拼接了~

```js
let a = {
    str:'模板字面量'
}
console.log('ES6' + a.str)
// ES6
console.log(`ES6${a.str}`);
```

* 换行直接按下键盘的Enter就可以了

```js
console.log('ES6\n模板字面量')
// ES6
console.log(`ES6
模板字面量`)
```
## 箭头函数
* ES6的箭头函数简化了函数的语法

```js
var plus = function (a, b){
    return a + b;
}
// ES6箭头函数
var plus = (a, b) => {
    return a + b;
}
// 或者这样
var plus = (a, b) => a + b;
```

* 箭头函数的this指向是固定的，即在箭头函数声明的时候就定义好了，继承来自外部最近的this指向

```js
var x = 7;
var obj = {
    x:77,
    print:function(){
        console.log(this.x);
    }
}
obj.print() // obj调用的，则this指向obj，77

var obj = {
    x:77,
    print:()=>{
        console.log(this.x);
    }
}
obj.print() // print是箭头函数，在声明的时候this就指向obj内部的this指向window，7 

function test(){
    this.x = 7777;
    let print = function (){
        console.log(this)
    };
    print();
}
test() // 全局调用this指向window，7

function test(){
    this.x = 7777;
    let print = () =>{
        console.log(this)
    }
    print();
}
test(); // 箭头函数print，print在定义的时候this就指向test，7777
```