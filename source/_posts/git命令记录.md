---
title: git命令
date: 2020-09-14 10:44:39
author: Mr-xu
img: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
top: false
cover: false
coverImg: https://cdn.jsdelivr.net/gh/Tokisaki-Galaxy/res/site/medias/background.jpg
toc: false
mathjax: false
summary: 记录git的常用命令
categories: Git
tags:
  - git
---

## 基本命令
``` javascript
  git init                    // 初始化git
  git clone <url>             // 克隆仓库
  git status                  // 查看状态
  git branch -a               // 查看本地所有分支
  git checkout [分支名]       // 切换分支
  git checkout -b [分支名]    // 创建并切换到分支
  git ls -files               // 查看已经提交
  git log                     // 查看提交记录
  git stash push              //将文件push到临时空间
  git stash pop               // 将文件从临时空间拉取下来
  git reset --hard [commit]   // 回退到指定提交同时清空暂缓区
  git revert <commit>          // 撤销指定的提交
  git rebase master           // 更新master到分支上
  git fetch origin             // 更新远程仓库到本地
```

## 本地新建文件并关联新仓库
``` javascript
  git init
  git add README.md
  git commit -m "first commit"
  git branch -M main // 设置本地分支名(看个人喜好)
  git remote add origin https://github.com/Mr-xu0810/xxxx.git
  git push -u origin main:master // 推送本地分支到远程
```

## 已有仓库变更其他仓库
``` javascript
  git remote rm origin   // 删除旧仓库地址
  git remote add origin 'https://github.com/Mr-xu0810/turn.git'
  git branch -M main // 设置本地分支名 可跳过
  git push -u origin main:master /  git push -u origin master
```