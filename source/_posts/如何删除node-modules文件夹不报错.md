---
title: 如何删除node_modules文件夹不报错
date: 2019-03-08 09:54:11
categories: [vuejs]
tags: [vuejs, 前端]
---
如果修改了文件路径和依赖包，npm有时候会出现报错的情况，怎么都修改不了

最好的方法也是最直接的办法就是删掉依赖包文件夹再重新安装依赖

但是在windows上经常会遇到需要依赖包删除需要用户权限，还经常删除失败

搜索了一圈 可以有这样的方法
```javascript
npm install rimraf -g

rimraf node_modules
```
省时省力  轻轻松松解决


### `rimraf` 命令是什么呢

根据[npm官网](https://www.npmjs.com/package/rimraf)上的说法是
> The UNIX command rm -rf for node   

有很多具体的用法，包括修改文件夹权限，回调等等，可以直接看官网文档，现在用到的就是快速有效删除依赖包文件夹

