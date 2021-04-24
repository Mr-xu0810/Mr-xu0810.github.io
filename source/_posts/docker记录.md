---
title: docker记录
date: 2020-12-03 20:21:39
author: Mr-xu
img: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
top: false
cover: false
coverImg: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
toc: false
mathjax: false
summary: docker使用过的命令记录及问题记录
categories: docker
tags:
  - 配置
---


## 基本命令
```
  docker ps -a  查看docker容器

  docker start 【containerId】运行容器

  docker stop 【containerId】停止容器

  docker rm 【containerId】删除容器

  docker inspect 【containerId】查看容器详情

  docker exec -it 【containerId】 /bin/bash 进入docker容器
```


## 问题记录

###### docker 进程提示： Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

**解决方法**：systemctl daemon-reload   // 重新加载配置服务文件

​					systemctl restart docker.service   // 重启docker服务