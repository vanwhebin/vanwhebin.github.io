---
title: django环境安装mysqlclient出错，安装对应依赖
date: 2019-10-05 15:49:19
tags: django, ubuntu, macOS
---
出错
```
ERROR: Command errored out with exit status 1:
     command: /var/www/html/DjangoBlog/ubuntuEnv/bin/python -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-install-lyq7rh0r/mysqlclient/setup.py'"'"'; __file__='"'"'/tmp/pip-install-lyq7rh0r/mysqlclient/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' egg_info --egg-base pip-egg-info
         cwd: /tmp/pip-install-lyq7rh0r/mysqlclient/
    Complete output (10 lines):
    /bin/sh: 1: mysql_config: not found
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-install-lyq7rh0r/mysqlclient/setup.py", line 16, in <module>
        metadata, options = get_config()
      File "/tmp/pip-install-lyq7rh0r/mysqlclient/setup_posix.py", line 51, in get_config
        libs = mysql_config("libs")
      File "/tmp/pip-install-lyq7rh0r/mysqlclient/setup_posix.py", line 29, in mysql_config
        raise EnvironmentError("%s not found" % (_mysql_config_path,))
    OSError: mysql_config not found
    ----------------------------------------
ERROR: Command errored out with exit status 1: python setup.py egg_info Check the logs for full command output.

```


```
sudo apt install libmysqlclient-dev
```

安装完对应的依赖就一切OK


安装python也有对应的依赖需要提前安装

```
sudo apt-get install build-essential checkinstall
sudo apt-get install libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev
libmysqlclient-dev  software-properties-common

```

源码安装的python，都会安装在/usr/local/ 文件夹下，
只要在`/usr/bin`将对应的python软链接修改为当前安装的版本即可

```
# 文件夹/usr/bin下

ln -s /usr/local/bin/python3.6  python
```



如果是centos，也有对应的依赖，对应安装即可

---
如果是MacOS出现对应的错误


第一， 先检查是否安装了`mysql-connector-c`，如果没有，先进行安装`brew install mysql-connector-c`， 也可以先进行卸载在重装 `brew unlink mysql-connector-c`
>>找到官方文档 https://github.com/PyMySQL/mysqlclient-python，解释说安装前需安装另一个模块：
`brew install mysql-connector-c`

第二，如果出现mysql_config not found错误，需要将mysql_config链接到/usr/local/bin下
`ln -s /usr/local/mysql/bin/mysql_config /usr/local/bin/mysql_config`， 可以使用`which mysql_config`查找对应的路径

第三， 如果继续出现安装失败，需要看下对应的mysql_config的配置项， 我这里是114行，将
```
libs="-L$pkglibdir"
libs="$libs -l "
```

修改为
```
libs="-L$pkglibdir"
libs="$libs -lmysqlclient -lssl -lcrypto"
```

如果出现找不到library ssl  或者是crypto的情况，需要显式支出mysql
`LDFLAGS=-L/usr/local/opt/openssl/lib pip install mysqlclient`


也有可能报错如下：
`ld: library not found for -lssl`
表示GCC找不到这个库
使用一下命令可以解决
```shell
brew install openssl
export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/opt/openssl/lib/ 
```
亲测可行， [githu issue来源](https://link.zhihu.com/?target=https%3A//github.com/brianmario/mysql2/issues/795)
