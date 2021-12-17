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

###### 一：上传一个本地的独立分支

1、git init （初始化环境，生成.git环境）
2、git add . （讲文件添加暂存区）
3、git commit -m “描述信息” （提交暂存区文件）
4、git branch 分支名称 （创建本地分支）
5、git checkout 分支名称 （切换到本地分支）
6、git remote add origin 远程仓库地址 （关联远程仓库）
7、git push origin 分支名 （推送本地分支到远程仓库）

###### 二：上传本地仓库到远程仓库指定分支

1、创建本地文件夹，并在次文件夹处打开Git Bash
2、git init （初始化环境，生成.git环境）
3、git remote add origin 远程仓库地址 （连接远程仓库）
4、git pull origin 远程仓库分支名 （拉取远程仓库指定分支）
5、git checkout --track origin/远程仓库分支名 （追踪远程仓库分支，与本地仓库建立联系）
6、在本地仓库中添加文件或修改文件
7、git add . (讲文件添加暂存区)
8、git commit -m ‘描述信息’ （提交暂存区文件）
9、git push origin 远程仓库分支名 (推送到远程仓库指定分支)