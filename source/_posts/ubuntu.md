---
layout: halo
title: 在ubuntu上将php7.0升级为php7.2
date: 2018-09-05 16:47:20
tags: php ubuntu
author: vanwhebin
---
心血来潮想使用lumen来进行开发, github上下载源码之后发现只能使用php7.1以上的版本
然后开始纠结是否要进行更新php版本。一直嫌麻烦但是终于还是动手了

```php

// 可以直接使用命令进行升级
// 先添加更新源

add-pat-repository ppa:ondrej/php
// 要先进行更新，否则找不到匹配
apt-get update

apt-get upgrade php

// 安装相应的php扩展
apt-get install php-gd
apt-get install php-dom
apt-get install php-mysql
apt-get install php-curl
apt-get install php-mbstring

// 如果提示没有相应扩展，要使用php7.2开头  比如php7.2-curl 或者php7.2-dom
```


> 很重要的一点，就是修改nginx或者是apache移交php处理的端口修改

记得更新php7.2之后要安装

```php
sudo apt-get install php-fpm
```
然后就可以修改nginx站点配置的fastcgi配置了
![更新后台的截图](https://i.loli.net/2018/09/05/5b8f9b4fd5392.png)


