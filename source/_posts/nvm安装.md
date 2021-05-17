---
title: nvm安装
date: 2020-09-09 19:44:39
author: Mr-xu
img: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
top: true
cover: false
coverImg: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
toc: false
mathjax: false
summary: 记录nvm的安装
categories: node
tags:
  - node
  - nvm
---

## Windows安装包安装nvm
  https://github.com/coreybutler/nvm-windows/releases 下载需要版本进行安装

## mac安装nvm
  >github地址： https://github.com/nvm-sh/nvm

  根据文档运行以下命令：
  ``` bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash

    wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
  ```

  会被墙，不太行，推荐使用git下载

    1. `cd ~/` (任意一个存储位置) 
    2. `git clone https://github.com/nvm-sh/nvm.git .nvm`  git拉取nvm整个仓库
    3. `cd ~/.nvm`
    4. `git checkout v0.38.0`  最新版是0.38.0，也可以切换其他版本
    5. 在clone的目录下运行`. ./nvm.sh` 
    6. .bashrc或者.zshrc中配置环境
      ```
        export NVM_DIR="$HOME/.nvm"
        [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
      ```
    7. 运行 `source ~/.bashrc 或者 source ~/.zshrc ` 重新加载配置文件

## nvm基本命令
  ``` bash
    nvm list                    //查看nvm安装的node
    nvm list available          //显示可以安装的所有node.js的版本
    nvm use <version>           //切换到使用指定的nodejs版本
    nvm install <version>       //安装node.js的命名 version是版本号 例如：nvm install 8.12.0
    nvm uninstall <version>     //卸载node.js是的命令，卸载指定版本的nodejs，当安装失败时卸载使用
    nvm version                 //查看当前的版本
  ```