---
title: uniapp 分享配置
date: 2021-05-03 19:23:46
author: Mr-xu
img: /images/5.jpg
top: false
cover: false
summary: uniapp开发中遇到需要分享功能，记录下实现过程
categories: vue  uniapp
tags:
  - 配置
---

# uniapp  分享设置：

>具体参数查看文档

### 1. 单独页面设置:  页面中onShareAppMessage（分享好友）和onShareTimeline（分享朋友圈）

### 2. 公用方法，通过mixins加入页面

   定义share.js：

    ```bash
       export const shareMixins = {
           data () {
               return {
                   shareData: {
                       title: '',
                       path: '',
                       imageUrl: '',
                       content: '',
                       desc: ''
                   },
       			circleData: {
       				title: '',
       				query: '',
       				imageUrl: ''
       			},
       			favoriteData: {
       				title: '',
       				imageUrl: '',
       				query: ''
       			}
               }
           },
       //#ifdef MP-WEIXIN
       onShareAppMessage () {
           return {
               title: this.shareData.title,
               path: this.shareData.path,
               imageUrl: this.shareData.imageUrl,
               content: this.shareData.content,
               desc: this.shareData.desc,
               success: res => {
                   console.info(res)
               }
           }
       },
       onShareTimeline() {
       	return {
       		title: this.circleData.title,
       		query: this.circleData.query,
       		imageUrl: this.circleData.imageUrl,
       		success: (res) => {
       			console.log(res);
       		}
       	}
       },
       onAddToFavorites() {
       	return {
       		title: this.favoriteData.title,
       		imageUrl: this.favoriteData.imageUrl,
       		query: this.favoriteData.query,
       		success: (res) => {
       			console.log(res)
       		}
       	}
       },
       //#endif
       
       onLoad(option) {
       }
    }
    ```

    第二步在需要的页面中引入并添加mixins

   ```bash
   export default {
   
   	data(){
   
   		return{
   
   			// 直接进行分享的参数配置 或进行另外的赋值操作
   
   		}
   
   	},
   
   	mixins: [shareMixins],
   
   }
   ```
