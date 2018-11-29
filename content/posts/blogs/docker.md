---
title: "Docker"
date: 2018-11-29T16:25:34+08:00
showDate: true
draft: false
tags: ["docker"]
---
记录学习docker的过程
## 特性
标准化
加速开发和构建流程，方便测试。容器可以在开发环境构建，轻松的提交到测试环境，并最终进入生产环境
## docker核心组件
* docker客户端和服务器（C/S）：docker引擎
* docker镜像
* 仓库Registry
* docker容器

## 安装
按照官网给的步骤一步一步来就好了
<br>https://docs.docker.com/install/

## 启动
```bash
$ systemctl start docker
```
## 运行一个容器
```
$ docker run -i -t centos /bin/bash
```
-i 开启标准输入(STDIN)
<br>-t 分配伪tty终端
设置了这两个参数就创建了一个我们可以交互的容器

## 附着到正在运行的容器
```bash
$ docker attach containerId/Name
```

## 删除容器
```
删除一个容器
$ docker rm containerId/Name

删除所有容器(-q是只显示容器id)
$ docker rm `docker ps -a -q`
```

## 镜像
拉取镜像
```bash
$ docker pull imageName:version
```

查看镜像详细信息
```bash
$ docker inspect repositoryName/imageId
```
## 登录
```bash
$ docker login
Username:~
Password:~
```
## 创建镜像
commit命令创建镜像
```bash
$ docker commit containerId/Name respositoryPath
```
Dockerfile创建镜像
```bash
$ mkdir buildEnv
$ cd buildEnv
$ touch Dockerfile
```
