---
title: docker+nginx部署vue项目
date: 2021-04-20 19:20:21
author: Mr-xu
img: /images/4.jpg
top: false
cover: false
summary: 学习下如何使用docker+nginx形式实现vue项目的部署
categories: vue
tags:
  - 配置
---

# docker+nginx部署vue

## 创建vue项目

1.安装vue cli:   

```bash
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

2.创建项目：

```bash
vue create hello-world
```

打包项目：

```bash
npm run build
```

## Nginx的config文件创建

nginx.conf文件编写

```bash
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    access_log  /var/log/nginx/host.access.log  main;
    error_log  /var/log/nginx/error.log  error;

    location / {
        root   /var/www/html/index.html;	# index.html放置的位置路径
        index  index.html index.htm; # 识别的index.html index.htm
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {  //
        root   /usr/share/nginx/html;  #错误页面的路径
    }
}
```



## Dockerfile 创建

1.创建dockerfile文件

​	项目根目录或其他路径下创建Dockerfile文件，编写内容：

```bash
FROM nginx     # 拉去nginx镜像
COPY ./dist /var/www/html			# 命令的意思是将项目根目录下dist文件夹下的所有文件复制到镜像中 /var/www/html/ 目录下
COPY ./default.conf /etc/nginx/conf.d/  # 命令的意思是将当前目录下的default.conf 复制到 etc/nginx/conf.d/下，用本地的 default.conf 配置来替换nginx镜像里的默认配置
EXPOSE 80
```

2.构建镜像

```bash
docker build -t 镜像名 .    // .表示的是 基于当前目录下的Dockerfile
```

3.运行容器

```bash
docker run -p 3000:80 -d --name vueApp 镜像  
// -p 3000:80 将宿主的3000端口映射到容器的80端口
// -d 表示后台运行
// vueApp 设置的容器名称
```
