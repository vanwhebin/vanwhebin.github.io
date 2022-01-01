---
title: 如何在centOS6.5 下手动安装php的redis扩展
date: 2018-07-20 12:19:37
author: vanwhebin
tags: php redis
---


- 安装环境：CentOS 6.5
- php版本：5.3.27
- redis扩展包版本：2.2.4
- redis安装包版本：2.6.14



#### 第一步：
获取准备好安装包

#### 第二步：
上传扩展包到php的拓展目录下 一般是 /usr/local/php/include/php/ext,解压后，看到文件config.m4，如果没有这个文件，后续操作可能会报错

#### 第三步：在加压后的扩展文件目录下，使用phpize来生成配置文件
/usr/local/php/bin/phpize 生成configure文件

#### 第四步：按照配置文件安装扩展，得到redis扩展最后的安装文件目录

```shell
./configure –with-php-config=/usr/local/php/bin/php-config

make && make install
```


#### 第五步：得到redis扩展包的最后的安装文件目录之后，在php.ini文件中修改配置项，打开redis扩展
如果没有相应的redis项，需要手动添加,



别忘记重启apache，就可以看到