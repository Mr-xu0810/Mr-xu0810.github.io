---
title: 移动端Date的差异
date: 2021-05-18 20:54:44
author: Mr-xu
img: /images/2.jpg
top: false
cover: false
summary: 移动端进行new Date转换时，ios和android对于参数有区别
categories: 移动端
tags:
  - 兼容
---

# 移动端在处理new Date转换时，对参数格式有不同的要求

>起因：在转换时间获取几分钟，几秒钟，几小时前的处理中，通过接口拿到数据中的时间格式为 2021-05-10 10:00:00，处理后在andorid上显示正常，而在ios上显示null

### 出现该情况的原因
  为什么会出现这种情况，主要在于android和ios的内核及处理格式不同导致了new Date在android和ios下有效格式不同，ios中new Date的处理格式只能是 2021/05/10 10:00:00, 对于连接符不是/的格式无法正常转换

### 解决办法
  将连接符统一转换为 '/' 
  ``` javascript
    var obj="2021-05-10 10:00:00".replace(/-/g, "/")
  ```