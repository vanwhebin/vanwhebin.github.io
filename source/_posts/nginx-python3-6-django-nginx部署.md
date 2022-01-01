---
title: nginx python3.6 django nginx部署
date: 2019-03-06 10:28:39
tags: django python nginx uwsgi
---

在使用python进行开发后，终于也实现了部署

出现的问题

出现无法加载app
配置文件写的不对 module项的配置不对，通常文件夹路径和app重名导致了误解
使用wsgi-file也要注意


!!! no internal routing support, rebuild with pcre support !!!
无法启动   libpcre3 
sudo apt-get install libpcre3 libpcre3-dev
pip uninstall uwsgi
sudo apt-get remove uwsgi

https://stackoverflow.com/questions/21669354/rebuild-uwsgi-with-pcre-support

uWSGI: No request plugin is loaded, you will not be able to manage requests

需要在配置文件里增加python插件支持
sudo apt-get install uwsgi-plugin-python
https://stackoverflow.com/questions/20176959/uwsgi-no-request-plugin-is-loaded-you-will-not-be-able-to-manage-requests


ImportError: No module named django.core.wsgi for uwsgi
虚拟环境问题
需要增加 虚拟环境的路径