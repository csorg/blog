---
title: chenshuaishizhu
date: 2017-10-14 22:31:44
tags:
---

# 博客发布流程

- 在e:\hexo 目录下右键打开gitbash

- 输入命令 

  ```
  git pull
  ```

- ### 创建一篇博客

  1. 输入命令

     ```
     hexo new "input blog name"
     ```

  2. 此时会在`E:\hexo\source\_posts`目录自动新建一篇你输入名字的博客文件，md格式

  3. 然后编写博客

- ### 发布博客

  1. 输入以下命令

     ```
     hexo clean
     ```

     ```
     hexo g
     ```

     ```
     hexo d
     ```

  2. 输入密码：123456

  3. 成功

- ### 删除博客

  直接进到博客文章文件夹删掉那个博客文档，然后按照`发布博客`的步骤执行一遍

- ### 同步文件到github

  依次输入以下命令：

  ```
  git add .
  git commit -m " "
  git push -u origin master
  ```

  ​