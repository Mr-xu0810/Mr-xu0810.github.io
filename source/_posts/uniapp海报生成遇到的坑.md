---
title: uniapp海报生成遇到的坑
date: 2021-05-29 19:51:34
author: Mr-xu
img: /images/5.jpg
top: false
cover: false
summary: uniapp生成海报，无法使用请求获取的base64图片
categories: uniapp
tags:
  - 问题
---

# uniapp生成海报问题
>在进行一个信息类型的使用uniapp完成的小程序中，需要进行海报分享的操作，需要生成海报，遇到了一些坑：

## 海报的样式
+ 使用canvas进行海报的绘制
由于不太会canvas就不详细展露自己的短板，具体可以网上查找

+ 使用uniapp的插件painter
  1.使用[海报生成工具](https://lingxiaoyi.github.io/painter-custom-poster/) 设计自己的海报样式，导出json样式
  2.[github下载插件](https://github.com/Kujiale-Mobile/Painter)
  3.在本地项目新建wxcomponents文件夹 将下载的components/painter文件夹复制进来
  4.本地项目pages.json中 globalStyle 属性下加入引入路径
  ``` javscript
    "globalStyle": {
      "usingComponents":{
          "painter":"/wxcomponents/painter/painter"
      }
    }
  ```
  5.在需要的地方引入,传入参数组件初始化自动生成 canvas图片
  ``` javascript
    <painter
      @imgOK="onImgOk"
      @imgErr="onImgErr"
      widthPixels="750"
      :customStyle="customStyle"
      :palette="template"
  />

  // palette => template 传入的json代码
  // onImgOk 海报生成成功的回调函数, e.detail.path 获取 生成的图片
  // onImgErr 海报生成失败的回调函数
  // widthPixels 强制指定生成的图片的像素宽度，否则，根据你画布中设置的大小来动态调节，此属性可以提高图片分辨率。
  // customStyle 设置生成的canvas图片样式
  ```

## 海报json配置项里无法使用base64图片
>解决方法： 缓存bease64为本地域名

``` javascript
  base64Save(base64File) { //base64File 需要加前缀
    const fsm = wx.getFileSystemManager();
    let extName = base64File.match(/data\:\S+\/(\S+);/)
    if (extName) {
      extName = extName[1]
    }
    let fileName = Date.now() + '.' + extName
    return new Promise((resolve, reject) => {
          let filePath = wx.env.USER_DATA_PATH + '/' + fileName
          fsm.writeFile({
                filePath,
                data: base64File.replace(/^data:\S+\/\S+;base64,/, ''),
                encoding: 'base64',
                success:(res)=>{
                      resolve(filePath);
                },
                fail() {
                reject('生成失败');
                },
          });
        });
  }
```