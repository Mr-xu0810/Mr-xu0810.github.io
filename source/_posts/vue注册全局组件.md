---
title: vue注册全局组件
date: 2021-12-09 20:11:02
author: Mr-xu
img: /images/3.jpg
top: false
cover: false
summary: 自定义组件时能够全局使用，且只需注册一次
categories: 自定义
tags:
  - vue
---

# VUE注册全局Message

> 简易的实现自己的message组件

## 定义组件样式

Message.vue

```vue
// template 部分
<template>
	<transition name="fade">
    <div class="message-box" v-if="flag">
        <i class="iconfont" :class="filterColor"></i>
        <span class="message-text">{{ text }}</span>
    </div>
</transition>
</template>
<script>
export default {
  name: 'Message',
  data() {
    return {
      type: '',
      text: 'this is long text',
      flag: false
    }
  }
}
</script>
<style>
    .fade-enter, .fade-leave-active {
      opacity: 0;
    }
    .fade-enter-active, .fade-leave-active {
      transition: opacity 0.3s;
    }
    .message-box {
      max-width: 500px;
      min-width: 50px;
      padding: 10px 20px;
      box-sizing: border-box;
      overflow: hidden;
      position: fixed;
      display: flex;
      flex-direction: row;
      justify-content: flex-start;
      align-items: center;
      top: 40px;
      left: 50%;
      transform: translateX(-50%);
      background-color: $white;
      box-shadow: 0 0 10px $shadow_color;
      border: 1px solid $content_title_bg;
      border-radius: 4px;
      z-index: 120;
      &>i {
        margin-right: 20px;
        font-size: 18px;
        color: $font_blue;
      }
      &>span {
        font-size: 16px;
        color: $main_color;
        line-height: 1.5;
        display: -webkit-box;
        text-overflow: ellipsis;
        overflow: hidden;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
      }
  }

</style>
```



## 组件注册

index.js ----注册组件方法

```javascript
import Vue from 'vue'
import CusMessage from './Message.vue'

const Message = Vue.extend(CusMessage)

CusMessage.install = (options) => {
  if (options === undefined || options === null) {
    options = {
      text: 'this is long text',
      type: ''
    }
  }
  if (typeof options === 'string' || typeof options === 'number') {
    options = {
      text: options,
      type: ''
    }
  }
  
  const instance = new Message({
    data: options
  }).$mount()

  document.body.appendChild(instance.$el)

  Vue.nextTick(() => {
    instance.flag = true
    setTimeout(() => {
      instance.flag = false
    }, 3000)
  })
}

export default CusMessage
```

main.js ---- 引入组件并注册

```javascript
import Vue from vue
import CusMessage from '@/views/components/cusMessage'

Vue.property.$cusMessage = CusMessage.install
```

这样就完成全局组件的注册



## 组件引用

```javascript
this.$cusMessage({
    type: 'success',
    text: 'this is long text'
})
```



> 后续学习更深后再进行更新