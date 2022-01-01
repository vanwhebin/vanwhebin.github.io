---
title: 如何将本地非空目录添加进入git仓库
date: 2019-12-28 16:22:28
tags: git
author: vanwhebin
---


## 一、本地：

- 1.将本地项目文件初始化成git版本库

    git init

- 2.将本地项目的文件添加到版本库中

    git add .

- 3.将添加的文件提交到版本库

    git commit -m '你的描述'

## 二、github网站：

- 4.在github中新建一个同名的仓库

## 三、本地：

- 5.给本地版本库设置远程仓库：

两种方式：

(1)使用ssh方式：

    git remote add origin git@github.com:zqunor/lamp.git

(2)使用http方式：

    git remote add origin https://github.com/zqunor/lamp.git

区别是ssh方式当把本地的ssh key公钥放到github上后就可以直接使用push和pull等操作，而http方式需要手动输入github账号的用户名和密码，进行验证

## 四、将本地版本库推送到github上

    git push origin master 

即可实现将本地已经存在的项目编成git仓库，并提交到github上进行版本控制管理

