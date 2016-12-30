---
layout:     post
title:      "Github Pages notes"
subtitle:   "技术文章编撰的相关说明"
date:       2016-12-29 12:00:00
author:     "戴伟来"
header-img: "img/post/Github Pages notes/2016-12-29-bg.jpg"
tags:
    - 教程
    - 说明
---



# Github Pages notes

## 前言

Github是目前(2016年12月30日)世界上最大的开源项目托管中心，在这里能够了解到最新的开源技术、能够认识最顶尖的开发者；对于一个技术爱好者以及开发者而言，这个社区是一个结合你的兴趣以及提升能力最佳的地方！

整个互联网世界的发展离不开开源力量的贡献，互联网的发展带给我们的社会以及文明的飞速发展，使得每一个人都获益良多！所以我们选择在这个开源世界的中心学习并且回馈社会！

当前的这个博客基于[Github Pages](){:target="_blank"}+[Jekyll](){:target="_blank"}搭建而成！下面是这个博客系统基本的用法说明。



## Github Pages

[Git技术](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000){:target="_blank"}、[Github](https://help.github.com/){:target="_blank"}、仓库、以及团队协作方面的知识本文不会赘述，请自行查阅相关的资料。

Github Pages可以理解为Github上一个仓库的说明文档，只要这个仓库中符合特定条件：如仓库更目录下有`index.html`，那么Github会为这个仓库自动生产Github Pages页面，其域名是`https://[用户名].github.io/[仓库命]`，如当前博客的仓库名是`izhangmai.github.io`，当前注册用户名为`izhangmai`，如下图

![](/img/post/Github Pages notes/pic1.png)

并且`izhangmai.github.io`仓库的主目录下有`index.html`文件。那么Github会自动为`izhangmai.github.io`这个项目生产Github Pages的页面，其链接地址为：`https://izhangmai.github.io/izhangmai.github.io`。

这里Github有一个特殊的Github Pages生成规则，即是当仓库名称为`[用户名].github.io`命名的，会自动以`https://[用户名].github.io`为Github Pages的链接地址。所以最终`izhangmai(当前登录用户名)`下的一个仓库`izhangmai.github.io`的Github Pages的地址为：`https://izhangmai.github.io`。

当前Github Pages已经默认是Enforce Https通信协议了。



## Jekyll

[Jekyll](){:target="_blank"}是一个博客构建工具，Github已经自带这个构建工具了，所以你不需要怎么特殊处理，只要你的仓库说明符合Jekyll的配置以及语法要求，Github会自动使用Jekyll来构建你仓库的Github Pages。

当然你也不希望发布出来的文章充满了排版bug，所以你可以在你自己的计算机安装Jekyll来对你将要发布的文章进行测试和预览，具体的方法请参阅Jekyll使用手册。



## 其他说明

当前的博客系统得到完整[Markdown](https://www.appinn.com/markdown/){:target="_blank"}语法支持，所以建议你使用Markdown进行博客书写！

每一篇文章就写成一个`.markdown`文件，**该文件的命名有一定要求，例如当前文章的文件名是：`2016-12-30-Github Pages notes.markdown`，其格式要求为：`年-月-日-文章标题.markdown` 并且必须放置在`/_posts`下才能正确被解析。**

其他资源文件(不支持视频！)的放置位置默认是没有限制的，但是为了项目的整洁，希望将所有资源放置的相应的位置！如图片资源请放置到`/img`目录下！

代码高亮使用[prism](https://prismjs.com/){:target="_blank"}，示例如下

``` objectivec
#import <Foundation/Foundation.h>  
int main()  {  
    NSLog(@"Hello World.");  
    return 0;  
}
```

每一篇文章都有头部`元数据`，其格式和说明如下：

```
layout:     布局样式，技术文章的话默认是post
title:      "文章标题，和文件名无关"
subtitle:   "文章副标题"
date:       日期，格式需严格要求
author:     "作者"
header-img: "当前文章的顶部封面资源"
tags: 标签
    - 教程
    - 测试tags
    
更多详情请参阅当前文章的头部元数据   
```



