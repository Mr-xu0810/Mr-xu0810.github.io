---
title: nginx
date: 2021-01-20 20:44:39
author: Mr-xu
img: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
top: false
cover: false
coverImg: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
toc: false
mathjax: false
summary: nginx的命令及路径配置
categories: nginx
tags:
  - 配置
---

## 查看nginx配置

  ``` bash
    ps -ef|grep nginx可以查看到nginx的进程
    /usr/sbin/nginx -t 查找主配置文件
    cat /etc/nginx/nginx.conf 可用查找配置文件路径
  ```

## nginx启动、重启、停止

  ``` bash
    cd /usr/local/nginx/sbin
    ./nginx  // 启动
    ./nginx -c /etc/nginx/nginx.conf 指定配置启动
    ./nginx -s reload  // 重新加载配置文件

    关闭
    ps -ef | grep nginx
    kill -9 nginx进程号
  ```

## nginx配置代理

  ``` bash
    server: {

    ​	listen    8080;

      server_name localhost;


      \#charset koi8-r;

      \#access_log /var/log/nginx/host.access.log main;

      location / {

    ​    root  /app/train-platform/dist;

    ​    index index.html index.htm;

      }

      location /web {

    ​    alias /app/train-platform-web/dist/;

    ​    index index.html index.htm;

      }

    }
  ```

**注意点**：**根访问的配置候用root/alias 指向 ； 分支访问的配置要用alias 来指向 ；否则无法代理成功**