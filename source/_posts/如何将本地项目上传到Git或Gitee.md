---
title: "如何将本地项目上传到Git或Gitee"
date: 2023-05-22 15:12:35
tags: Git
categories: 随笔
link: git-push
---
### Git提交常用命令
1、初始化git
git init
2、将项目的所有文件添加到缓存中
git add .
3、将缓存中的文件Commit到git库
git commit -m "init"
4、将本地的库链接到远程仓库
git remote add origin 远程仓库地址复制代码
5、拉取远程仓库代码
git pull origin master
6、提交代码
git push origin master

<!-- more -->
### 遇到问题的解决方法
1、fatal: remote origin already exists.
- 解决方法：
  先输入 git remote rm origin
  再输入 git remote add origin 远程仓库地址复制代码

2、git pull 失败 ,提示：fatal: refusing to merge unrelated histories
- 解决方法：
- 方案一
  git pull origin master --allow-unrelated-histories
  后面加上 --allow-unrelated-histories ， 把两段不相干的 分支进行强行合并
  后面再push就可以了
- 方案二
  git push -f -u origin master 强推至远程服务器    上述方式会强制删除远程仓库中冲突代码，即删除创建的README.md文件，不推荐
