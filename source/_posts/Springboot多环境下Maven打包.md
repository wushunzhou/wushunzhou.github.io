---
title: Springboot多环境下Maven打包
date: 2023-06-01 13:32:40
tags: 后端
categories: Springboot
---
### springboot多环境下maven打包

[教程地址](https://www.cnblogs.com/fnlingnzb-learner/p/11042562.html)

### 灯塔环境使用这个

基于maven的springboot多环境yml配置文件切换与隔离：[教程](https://blog.csdn.net/bbcckkl/article/details/89882074)

<!-- more -->

### 案例示范

执行命令： mvn clean package -P china -Dmaven.test.skip=true -U

![avatar](https://img.wuzhouboy.top/blog/af7f59b7d4f4_40.png)

![avatar](https://img.wuzhouboy.top/blog/af7f59b7d4f4_40-1.png)


