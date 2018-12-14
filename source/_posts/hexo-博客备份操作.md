---
title: hexo 博客备份操作
date: 2018-12-14 09:32:22
categories: hexo
tags:
    - 博客
    - 备份
---
通过git分支来进行保存hexo源文件和静态网页。

<!--more-->

# 备份源文件

github pages 服务以master分支作文静态网页。所以建立新分支进行源文件保存，更改仓库默认分支为新分支，以后丢失或者或机器可以直接git clone。
hexo 分支源文件保存,master分支静态网页。
建立hexo分支 `git checkout -b hexo`

建立备份
```
git add .
git commit -m "hexo backup"
git remote add origin git@github.com:xunnun/xunnun.github.io.git
git push origin hexo
```
# 日常操作

发布新文章

保存新文件
```
git add .
git commit -m 'hexo backup'
git push origin hexo
```
发布部署静态网页
`hexo d `

# 文件丢失

```
git clone git@github.com:xunnun/xunnun.github.io.git
npm install hexo-cli
npm install
npm install hexo-deployer-git
```

