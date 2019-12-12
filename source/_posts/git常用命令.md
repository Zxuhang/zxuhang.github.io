---
title: git常用命令
date: 2018-06-12 10:56:59
tags: git
categories: git
---
# git
<!--more-->
```bash

//克隆
git clone git@地址

//查看状态
git status

//查看本地和远程分支，当前分支
git branch -a

//创建文件 test.text
touch test.txt

//添加修改到本地仓库
git add .

//本次提交注释
git commit -m "注释内容"

//查看远程仓库
git remote -v

//推送到远程主分支（master）
git push origin master

//创建新的分支(复制master分支内容)
git checkout -b 分支名称

//切换到master分支
git checkout master

//拉取别的分支到master分支合并分支（可能会冲突）
git merge 分支名称

//删除本地分支
git branch -D 分支名

//删除远程分支
git push origin :分支名

//回退上次提交
git reset --hard head^

//查看提交日志(git log)
git reflog

//回退1 谨慎使用 指定的提交（执行git reflog 查看版本号）复制指定的版本号 
git reset --hard 版本号

//回退2 通过反做创建一个新的版本，这个版本的内容与我们要回退到的目标版本一样
git revert 版本号
git revert OLDER_COMMIT^..NEWER_COMMIT
```