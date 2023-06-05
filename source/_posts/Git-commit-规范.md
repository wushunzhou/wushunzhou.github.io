---
title: Git commit 规范
date: 2023-05-29 11:37:21
tags: Git
categories: 随笔
link: git-commit-norm
---
## Commit 提交前缀规范

### 提交类型（type）用于说明此次提交的类型，需要指定为下面其中一个：

·feat：引入新功能

·fix：修复bug

·styie：更新UI样式文件

·format：格式化代码

·docs：添加／更新文档

·perf：提高性能／优化

·init：初次提交／初始化项目

<!-- more -->

·test：增加测试代码

·refactor：改进代码结构／代码格式

·patch：添加重要补丁

·file：添加文件文件

·publish：发布新版本［新版本］

·tag：发布版本／添加标签

·config：修改配置文件［配置）

·git：添加或修改.gitignore文件［不可见］

·chore：构建过程或辅助工具的变动

·ci：对CI配置文件和脚本的更改

·revert：恢复（Revert a commit），是把这次提交的修改给还原

### 作用域

作用域（scope）表示此次提交影响的范围。比如可以取值api，表明只影响了接口。

![avatar](https://img.wuzhouboy.top/blog/b63cffab8b5a_21.jpeg)
