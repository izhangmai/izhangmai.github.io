---
layout: post
title:  "【Docker】Docker简介与安装"
categories: 技术
tags:  Docker 虚拟化 分布式 容器
author: 胖纸囧
---

* content
{:toc}

记得2015年的某个夏天，那时候我还是个胖屌丝，拉着屌丝基友去参加开源中国的成都源创汇，碰到了张小龙，哦不，是张海龙大哥来推广Docker，那时候我怀着一颗敬畏的心满怀激情满脑懵逼的跟着海龙哥徜徉在Docker的海洋中，虽然直到听完我都不晓得Docker是个撒子。
结果17年开头的胖屌丝就不得不入Docker的坑了，开始了苦逼的Docker踩坑之旅。











## 简介

   Docker是一个能够把开发的应用程序自动部署到容器的开源引擎。由Docker公司([点击我](http://www.docker.com),前dotCloud公司，PaaS市场中的老牌提供商)的团队编写，基于Apache2.0开源协议发行。
    相对于其他的容器呢，Docker有以下特点：
    
* 提供了一个简单、轻量的建模方式
* 职责的逻辑分离
* 快速、高效的开发生命周期
* 鼓励使用面向服务的架构

## 核心组件

   Docker有以下几个核心组建组成：
    
* Docker客户端和服务器
* Docker镜像
* Regstry
* Docker容器

    这些组件在下面使用的过程中基本上都会用到。
    
## 作用

   扯了这么多，我们到底能拿Docker来干撒:

* 加快本地开发和构建流程，使其更加高效、更加轻量化。本地开发人员可以构建、运行并分享Docker容器。容器可以再开发环境中构建，然后轻松地提交到测试环境中，并最终进入生产环境。
* 能够让独立服务或应用程序在不同的环境中，得到相同的运行结果。这一点再面向服务的架构和重度依微型服务的部署中尤其实用。
* 用Docker创建的隔离环境来测试。例如，用Jenkins，CI这样的持续集成工具启动一个用于测试的容器。
* Docker可以让开发者先在本机上构建一个复杂的程序或者架构来进行测试，而不是一开始就在生产环境部署，测试。
* 构建一个多用户的平台即服务（PaaS）基础设施。
* 为开发、测试提供一个轻量级的独立沙盒环境，或者将独立的沙盒环境用于技术教学，如Unix shell的使用、编程语言教学。
* 提供软件即服务（SaaS：掌麦正在做的这种）应用程序，如Memcached即服务。
* 高性能、超大规模的宿主机部署。
    
    现阶段呢，我们只是拿Docker来统一开发测试环境，用prod环境的配置搭起dev，test，beta的开发环境。

## 安装

###### MacOS
    
   下载安装包直接安装（[点击我](https://download.docker.com/mac/stable/Docker.dmg)）
   
###### Liunx

1.centos

```
yum install docker
```

2.ubuntu

```
apt-get install docker
```

###### windows

下载安装包直接安装（[点击我](https://download.docker.com/win/stable/InstallDocker.msi)）

## 运行

###### MacOS
    
   点击Docker
   
###### Liunx
   
   
```
    service docker start

```

###### windows
  
  双击Docker

然后在命令行运行

```
    docker info
    
```
如果如下图所示的话，骚年，恭喜你，你的Docker安装成功了！！！
![](/img/post/Docker/QQ20170112-0.png)








