---
title: uniapp引入iconfont报错处理
date: 2021-05-09 19:37:54
author: Mr-xu
img: /images/1.jpg
top: false
cover: false
summary: uniapp引入iconfont后，在打包小程序后会有报错，导致页面白屏，记录解决方法
categories: vue  uniapp
tags:
  - uniapp
  - 问题
---

# uniapp引入iconfont 打包后会有报错，导致页面白屏

在将iconfont下载到本地的压缩包里会有iconfont.js文件，引起的错误的来源就是该文件内的元素存在被未被查找，导致在解析的时候就被报错阻断，无法完成正常解析，导致页面渲染失败

>解决方法： 第一种是在引入的iconfont文件夹下找到iconfont.js文件，删除该文件后即可正常使用  第二种将下载本地的iconfont文件不放入static里面，单独新建一个iconfont文件夹放入，在全局引入
