---
title: vue-quill-editor配置使用
date: 2021-01-07 19:24:09
author: Mr-xu
img: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
top: true
cover: false
coverImg: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
toc: false
mathjax: false
summary: 根据需求对vue-quill-editor进行配置
categories: vue
tag:
  - vue
  - vue-quill-editor
  - 配置
---

## Vue-quill-editor 添加代码高亮及图片上传

  > **vue-quill-editor** github地址：[https://github.com/surmon-china/vue-quill-editor](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fsurmon-china%2Fvue-quill-editor)
  >
  > **Highlight**  github地址：https://highlightjs.org/download/

#### 安装highlight.js

  ```
    npm install highlight.js
  ```

#### 配置高亮

  - main.js中引入样式文件
    ```
      import 'highlight.js/styles/monokai-sublime.css'; // 代码高亮样式
    ```

  - 组件内配置高亮
    ```
      // js
      import hljs from 'highlight.js';

      // data 数据部分
      editorOption: {
        modules: { 
          toolbar: [
            ["bold", "italic", "underline", "strike"], 
            ["blockquote", "code-block"], 
            [{ header: 1 }, { header: 2 }], 
            [{ list: "ordered" }, { list: "bullet" }], 
            [{ script: "sub" }, { script: "super" }], 
            [{ indent: "-1" }, { indent: "+1" }], 
            [{ direction: "rtl" }], 
            [{ size: ["small", false, "large", "huge"] }], 
            [{ header: [1, 2, 3, 4, 5, 6, false] }], 
            [{ color: [] }, { background: [] }], 
            [{ font: [] }], [{ align: [] }], 
            ["clean"], ["link", "image", "video"]
          ],
          syntax: { 
            highlight: text => { 
              return hljs.highlightAuto(text).value; // 这里就是代码高亮需要配置的地方 
            }
          }
        }
      }
    ```
#### 配置图片上传

  ```
    editorOption: {               //符文本编辑器的配置
      placeholder: '',
      theme: 'snow',
      modules: {
        toolbar: {
          container: [             // 工具栏配置, 默认是全部
            ["bold", "italic", "underline", "strike"], 
            ["blockquote", "code-block"], 
            [{ header: 1 }, { header: 2 }], 
            [{ list: "ordered" }, { list: "bullet" }], 
            [{ script: "sub" }, { script: "super" }], 
            [{ indent: "-1" }, { indent: "+1" }], 
            [{ direction: "rtl" }], 
            [{ size: ["small", false, "large", "huge"] }], 
            [{ header: [1, 2, 3, 4, 5, 6, false] }], 
            [{ color: [] }, { background: [] }], 
            [{ font: [] }], [{ align: [] }], 
            ["clean"], ["link", "image", "video"]
          ],
          handlers: {
          'image': function (value) {
              if (value) {
                // 给个点击触发input框选择图片文件
                document.querySelector('#quill-upload').click()
              } else {
                this.quill.format('image', false);
              }
            }
          }
        },
        syntax: { 
          highlight: text => { 
            return hljs.highlightAuto(text).value; // 这里就是代码高亮需要配置的地方 
          }
        }
      }
    }
  ```
  可以创建一个隐藏的上传控件

  ```
    <input type="file" id="#quill-upload" style="display: none" @change="uploadImg"/>  
  ```

  然后在配置的方法里配置状态栏点击图片时触发这个隐藏的上传控件来选择图片并自定义上传方法