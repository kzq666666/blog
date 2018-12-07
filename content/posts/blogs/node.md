---
title: "Node"
date: 2018-11-27T17:04:59+08:00
showDate: true
draft: false
tags: ["Node"]
---
开此篇记录下学习node的过程和一些笔记
1.事件驱动、非堵塞、单线程
2.Node.js是一个非阻塞的系统，当调用一些需要阻塞的等待或者事件，node会采用回调函数替代闲置等待，即事件驱动。就像我们在学校经常吃饭点餐的情况，点完餐之后店家会给个小票，上面有这此点餐的号码，到时候菜做好了就会叫号，这个号码相当于回调号码，这样就提高了效率，继续为下一个客人服务。
3.串行IO和并行IO，类似于同步和异步，前者的运行顺序是固定的，后者任何一个IO操作返回时间都是不确定的，如果IO操作有关联的话就要使用串行IO。按顺序的串行请求，无序的并行的请求