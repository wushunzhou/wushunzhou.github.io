---
title: 全新部署Jenkins之iOS篇-Mac
date: 2023-06-05 10:17:37
tags: Git
categories: 随笔
top: 2
---

Jenkins官网安装方法：https://www.jenkins.io/zh/download/


## 一、安装Jenkins

```java
# 默认最新LTS版本，可以指定版本号 brew install jenkins-lts              
```

接下来等待安装完成即可，默认端口为8080。一般8080端口会被占用，此时就需要修改端口号了。

## 二、修改Jenkins端口号的方法：

1. 打开终端，cd 到Jenkins的安装目录（即jenkins.war所在目录），如：

```java
cd /usr/local/opt/jenkins-lts/libexec/
```

<!-- more -->

2. 执行命令：“java -jar jenkins.war --ajp13Port=-1 --httpPort=9099” 执行完成后。

如果出现以下画面。表示端口修改成功，并同时启动了Jenkins服务。
![](https://img.wuzhouboy.top/blog/f4f3d60b-5a2a-4435-8356-683c4a27b277.png)

## 三、启动/关闭Jenkins服务
1. 启动Jenkins服务命令

   ```
   net start jenkins
   ```

2. 停止Jenkins服务命令

   ```
   net stop jenkins
   ```



## 四、首次登陆Jenkins需要通过密钥登陆，随后创建管理员账号

1、打开web界面输入密钥（如下图的这串字符串）
![](https://img.wuzhouboy.top/blog/77e78af4-fbbb-4a76-b4b2-05066fad4dc5.png)

2、创建管理员账号

![](https://img.wuzhouboy.top/blog/8941dbc8-b986-4a7c-a81b-708f33b9f5d9.png)

## 五、安装相应的插件。

1、直接选择推荐插件进行下载安装
![](https://img.wuzhouboy.top/blog/16b77866-5ac2-4417-ad93-e447cf70cbfa.png)

2、安装iOS打包必备的插件

路径：Manage Jenkins-> Manage Plugins ->进入到插件管理，搜索以下2个必备插件->安装重启Jenkins使之生效



**1、**[**Keychains and Provisioning Profiles Management**](https://links.jianshu.com/go?to=https%3A%2F%2Fupdates.jenkins.io%2Fdownload%2Fplugins%2Fkpp-management-plugin%2F1.0.0%2Fkpp-management-plugin.hpi)**（管理本地的keychain和iOS证书的插件）**

**2、**[**Xcode integration**](https://links.jianshu.com/go?to=https%3A%2F%2Fupdates.jenkins.io%2Fdownload%2Fplugins%2Fxcode-plugin%2F2.0.4%2Fxcode-plugin.hpi) **（用于xcode构建**）

![](https://img.wuzhouboy.top/blog/35ecabc7-810e-487a-b7ec-24e887f4889e.png)

## 六、新增凭证

![](https://img.wuzhouboy.top/blog/eeab1865-1e80-4484-a276-174bf5538788.png)

## 七、新建流水线，接下来的操作就是流水线+打包脚本「END」


![](https://img.wuzhouboy.top/blog/d8b9361c-82b1-4553-acaa-14007781bb0b.png)

## 八、Jenkins创建一个用户token，如下图，用户没有token

https://blog.csdn.net/xujiamin0022016/article/details/103484563

![](https://img.wuzhouboy.top/blog/50dc98e2-175c-443d-bcc2-c2e21beb8de3.png)

解决方法：

![](https://img.wuzhouboy.top/blog/037405eb-a0a4-4148-a349-ccf016001bcd.png)

## 九、QA补充

\# Q: LTS版本与jenkins正常版本STS的区别：

支持的时间以及稳定性不同，正常我们应该使用LTS为好，理由如下：

1、所有LTS版本(12.04和更高版本)在桌面和服务器上都支持五年。

2、所有正常版本(13.04及更高版本)仅支持9个月。

参考：https://blog.csdn.net/weixin_39692830/article/details/116908912

\# Q： 打包出现如下报错：

```
no known implementation of class jenkins.tasks.SimpleBuildWrapper is named BuildUser
```

![](https://img.wuzhouboy.top/blog/069d55a5-36d9-43be-931e-f716f1c2066f.png)

解决方法：这里因为jenkins没有安装plugin([user build vars plugin](http://wiki.jenkins-ci.org/display/JENKINS/Build+User+Vars+Plugin)) 一个环境变量插件

\# Q： 如何查看jdk安装路径以及版本：

![](https://img.wuzhouboy.top/blog/89846e74-07cd-45b0-8ea5-5735b9c66548.png)

[**【Linux】Jenkins以war包运行及开机启动配置（四）**](https://www.cnblogs.com/h--d/p/11186529.html)

https://www.cnblogs.com/h--d/p/11186529.html

账号分配并设置权限：

https://www.jianshu.com/p/f1d378596a67

https://blog.csdn.net/wanglei_storage/article/details/78339409

jenkins 跨域请求403问题描述

https://segmentfault.com/a/1190000040706914

解决方法：

https://blog.csdn.net/hiXavier/article/details/109047457

启动时

```
nohup java -jar -Dhudson.security.csrf.GlobalCrumbIssuerConfiguration.DISABLE_CSRF_PROTECTION=true  /usr/local/jenkins/jenkins.war --httpPort=8088 -DJENKINS_HOME=/usr/local/jenkins --webroot=/usr/local/jenkins/war --logfile=/usr/local/jenkins/jenkins.log &
```

正确使用java版本启动

```
/Library/Java/JavaVirtualMachines/jdk-11.0.2.jdk/Contents/Home/bin/java -jar -Dhudson.security.csrf.GlobalCrumbIssuerConfiguration.DISABLE_CSRF_PROTECTION=true /usr/local/opt/jenkins-lts/libexec/jenkins.war --ajp13Port=-1 --httpPort=9099
```



![](https://img.wuzhouboy.top/blog/4543a026-8d9d-4be3-9d5f-5aa30500d60e.png)



jdk 安装

https://www.jianshu.com/p/6273e7ab0c56

jdk切换使用

https://www.cjavapy.com/article/91/



**后台启动：**

```
nohup /Library/Java/JavaVirtualMachines/jdk-11.0.2.jdk/Contents/Home/bin/java -jar -Dhudson.security.csrf.GlobalCrumbIssuerConfiguration.DISABLE_CSRF_PROTECTION=true /usr/local/opt/jenkins-lts/libexec/jenkins.war --ajp13Port=-1 --httpPort=9099 &              
```

