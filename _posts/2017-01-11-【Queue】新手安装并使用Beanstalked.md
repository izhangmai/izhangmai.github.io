---
layout: post
title:  "【Queue】新手安装并使用Beanstalked"
categories: 技术
tags:  Queue Beanstalked
author: 胖纸囧
---

* content
{:toc}

因为公司项目准备要重构，根据当前业务的复杂度，为了降低系统业务耦合程度，需要在项目中引入消息队列机制。

## 资料

在使用之前先来点资料普及下什么是消息队列，还有消息队列有什么用：

- [消息队列](http://baike.baidu.com/link?url=JOv29wGjBmYc32hlY9v8yAfcs925V0mA5n-ZBVUcNu_JMSr1Xkd0I4t6Uby0us5y_JFAU4a71QWUf16QyOv4SzIidc1YZ2G7ho5GO0u-42WnCMS--rflOrw4nZlS4zUX)
- [消息队列有什么用？](https://segmentfault.com/q/1010000005780973)
- [PHP实现队列及队列原理](http://www.phpddt.com/php/queue.html)
- [大型网站架构之分布式消息队列](http://blog.csdn.net/shaobingj126/article/details/50585035)

## 候选

在当前的技术前景下，有以下几种队列选择：

- [JMS](http://baike.baidu.com/link?url=U2WYoeoyDZ1UdtsINkRQObR9rrDRviRDI9gfMpZ1QWl8mhAz5b20FfsYYyFEqF1Y2we9KJ4VMCso4uYziIVn_K)
- [RabbitMQ](http://www.rabbitmq.com)
- [ZeroMQ](http://www.zeromq.org)
- [Kafka](http://kafka.apache.org)
- [beanstakd](http://kr.github.io/beanstalkd/)

## 核心

Beanstalkd设计里面的核心概念：

* job
* tube
* producer
* consumer

## 安装

###### MacOS
    
    `brew install beanstalkd`
    
###### Linux-编译

1.安装libevent（[点击我](https://github.com/izhangmai/queue/blob/master/beanstalkd/package/beanstalkd-1.10.tar)）

```
wget http://cloud.github.com/downloads/libevent/libevent/libevent-1.4.14b-stable.tar.gz
cp libevent-1.4.14b-stable.tar.gz /usr/local/src/ 
tar zxvf libevent-1.4.14b-stable.tar.gz 
cd  libevent-1.4.14b-stable 
./configure --prefix=/usr/local/libevent 
make 
make install 
```

2.安装beanstalkd（[点击我](https://github.com/izhangmai/queue/blob/master/beanstalkd/package/beanstalkd-1.10.tar)）
    

```
cp beanstalkd-1.4.6.tar.gz /usr/local/src/ 
tar zxvf beanstalkd-1.4.6.tar.gz 
cd  beanstalkd-1.4.6 
./configure --prefix=/usr/local/beanstalkd 
make 
make install 
./beanstalkd -d -l 127.0.0.1 -p 11300 
```

######Liunx-包安装

1.centos

```
yum install beanstalkd
```
2.ubuntu

```
apt-get install beanstalkd
```

###### windows

windows果然是后娘养的，暂时没有官方提供的安装包只有国人修改的客户端，大家有兴趣的可以看看：[点击我](https://git.oschina.net/lomox/beanstalkd-win)

## 运行

1.首先cd到Beanstalkd目录(配好环境变量的哥子除外)
2.后台启动

```
beanstalkd -l 地址 -p 端口号 -z 最大的任务大小(byte) -c &
```

```

-b DIR   wal directory

-f MS    fsync at most once every MS milliseconds (use -f0 for “always fsync”)
-F       never fsync (default)
-l ADDR  listen on address (default is 0.0.0.0)
-p PORT  listen on port (default is 11300)
-u USER  become user and group
-z BYTES set the maximum job size in bytes (default is 65535)
-s BYTES set the size of each wal file (default is 10485760)
(will be rounded up to a multiple of 512 bytes)
-c       compact the binlog (default)
-n       do not compact the binlog
-v       show version information
-V       increase verbosity
-h       show this help
```

## Demo（[点击我](https://github.com/izhangmai/queue/blob/master/beanstalkd/index.php)）

```
<?php
    // 引入BeanStalk客户端类
    require('BeanStalk.class.php');

    $beanstalk = BeanStalk::open(array(
        'servers'       => array( '127.0.0.1:11300' ),
        'select'        => 'random peek'
    ));
    
    $beanstalk->use_tube('foo');
    
    $beanstalk->put(0, 0, 120, 'say hello world');
     $beanstalk->watch('foo'); 
    $job = $beanstalk->reserve_with_timeout(); 
    echo $job->get();
    Beanstalk::delete($job);

```


