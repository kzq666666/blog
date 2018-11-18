---
title: "Command"
date: 2018-11-17T13:49:47+08:00
showDate: true
draft: false
tags: ["command","git","linux"]
---
```js
Linux基本操作
ls -ah	查看所有文件,包括隐藏文件
pwd	print working directory 打印当前路径
mv oldname.js newname.js   重命名
cat		查看当前文件
cp:
	cp <file> <path>	复制file到path路径
	cp <file> <copy_name> 复制file并命名为copy_name,到当前路径
touch <file>  创建一个文件
rm -f <file> 删除一个文件
rm -rf <file package> 删除一个文件夹

-----------------------------------------------------------------
git基本操作
git是分布式版本控制系统
git 基本操作
git init 初始化仓库
git add	<file> 添加file到仓库暂存区
git commit		将暂存区的内容提交到master
git status		获取当前的git状态,查看哪些文件操作过
git diff <file>  查看file更改的详细信息
git log			查看当前git的信息
git reset --hard HEAD^  回退到HEAD之前的一个版本
git reflog 查看提交的不同版本commit号和具体信息
git checkout --<file>  	还没有进行git add <file>的操作,回退该文件最近提交的一个版本
git reset HEAD <file>   进行了git add <file>的操作,先进行该步操作,然后再使用git checkout --<file>
git rm	删除一个仓库的文件并且提交git commit
ssh-keygen -t rsa -C "youremail@example.com"  查看本地的ssh
git remote add origin <github上创建的目录的ssh>  远程连接库和本地库
git push -u origin master 将本地的文件全部上传到远程仓库中
之后可以直接用git push 上传文件


查看GitHub上的html文件 加上前缀http://htmlpreview.github.io/?

------------------------------------------------------------------
nginx
nginx.conf 配置文件
nginx -s reload 重启nginx

```











