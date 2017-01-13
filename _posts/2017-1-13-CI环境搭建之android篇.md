---
layout: post
title: "[linux]CI环境搭建之android篇"
date: 2017-1-13 16:00:00
author: 李勇
tags: android
---


## 可持续集成（CI）之起源篇

### 背景介绍
随着软件开发复杂度的不断提高，团队开发成员间如何更好地协同工作以确保软件开发的质量已经慢慢成为开发过程中不可回避的问题。尤其是近些年来，敏捷（Agile） 在软件工程领域越来越红火，如何能再不断变化的需求中快速适应和保证软件的质量也显得尤其的重要。 持续集成正是针对这一类问题的一种软件开发实践。

### 是什么
它倡导团队开发成员必须经常集成他们的工作，甚至每天都可能发生多次集成。而每次的集成都是通过自动化的构建来验证，包括自动编译、发布和测试，从而尽快地发现集成错误，让团队能够更快的开发内聚的软件。

## 可持续集成（CI）之搭建篇
CI环境采用jenkins+svn+jdk+sdk+gradle+fir搭建

### jdk
#### 安装
通过官方下载安装[jdk](http://java.com/) 
#### 配置
jdk环境变量配置：  
1. 编辑文件  
```vim /etc/profile```  
2. 添加环境变量  

```  

    JAVA_HOME=/此处为jdk目录路径/jdk1.8.0_111    
	JRE_HOME=/此处为jdk目录路径/jdk1.8.0_111/jre  
    CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib  
    PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin  
    export JAVA_HOME JRE_HOME CLASS_PATH PATH  
```    
3. 退出（ESC）,并保存（：wq+Enter）  
4. 将配置文件刷入内存  

```source /etc/profile```

### jenkins
#### 安装
从 Jenkins 的主页上下载最新的 jenkins.war 下载，命令：
```wget http://mirrors.jenkins-ci.org/war/latest/jenkins.war```
#### 配置
Jenkins默认端口为8080，易与其他服务端口冲突，此处改为8000作为jenkins访问端口（具体由情况而定），访问该端口，需要打开8000端口防火墙  

```
iptables -I INPUT -p tcp --dport 8000 -j ACCEPT
```

#### 启动jenkins
进入jenkins.war目录下，输入命令  
```
java -jar jenkins.war  --httpPort=8000
```

#### 访问jenkins
http://locahost:8000,若非本机则将locahost替换为jenkins所在主机ip地址，效果如图

![](/img/post/jenkins_android/jenkins_longin.png)

输入账号即可登录

### svn
登录jenkins，安装插件Subversion Plug-in

### sdk 

#### 安装
通过官方下载安装[sdk](https://developer.android.com/index.html)  

#### 配置
sdk环境变量配置：  
1. 编辑文件 
```vim /etc/profile```  
2. 添加环境变量  
```   

    export ANDROID_HOME=/此处为sdk目录路径/sdk
	export PATH=$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$PATH
  
```    
3. 退出（ESC）,并保存（：wq+Enter）  
4. 将配置文件刷入内存  
 
```source /etc/profile```

### gradle

#### 安装
通过官方下载安装[gradle](https://gradle.org/gradle-download/),此处选择gradle-2.14.1

#### 配置
gradle环境变量配置：  
1. 编辑文件 
```vim /etc/profile```  
2. 添加环境变量  
```   

    export GRADLE_HOME=/此处为gradle目录路径/gradle-2.14.1
	export PATH=$GRADLE_HOME/bin:$PATH

  
```    
3. 退出（ESC）,并保存（：wq+Enter）  
4. 将配置文件刷入内存  
 
```source /etc/profile```

### fir
通过 fir-cli 命令行的指令查看、上传、编译应用
#### 安装  
fir-cli 使用 Ruby 构建，只要安装相应 ruby gem 即可:  

```sudo gem install fir-cli --no-ri --no-rdoc```

***
至此CI环境所需工具及插件安装配置完毕。  

## 可持续集成（CI）之使用篇
1.登录进入jenkins主页，点击“新建”，创建项目

![](/img/post/jenkins_android/jenkins_create.png)

2.配置项目版本环境
创建项目成功后，进入项目配置页面，配置项目版本参数

![](/img/post/jenkins_android/jenkins_svn.png)

3.配置构建参数
配置编译、打包、上传分发平台参数

![](/img/post/jenkins_android/jenkins_build.png)

***
至此项目基础配置完成，可实现项目构建，并分发。

