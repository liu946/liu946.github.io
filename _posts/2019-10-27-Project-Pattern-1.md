---
layout: plain
title: 项目模式（一）—— 概述
category: tech
---

说来惭愧，研究生本来就在一个研究性非常强的实验室，毕业之后又来到了研究岗位，可是直到目前（19年11月），都在做一些工程相关的工作，从0或非从0开始写了一些系统，个人对于软件系统有一些感受和经验，就先如此记录下来，以便之后少走弯路。

### 项目模式及其应用范围

关于我为什么要把我想写的东西叫做项目模式，其实是深思熟虑的结果，正好在此明确一下这个系列的定位。

在我遇到一些项目模式的问题时，一开始，我觉得这应该是架构问题。去知乎上查了一些架构类的书籍，发现其都是描述项目之间的组织形式的，为了完成某一个任务，多个软件之间应该如何分配任务、合作，我更想要的是软件内部对模块、类的组织。我觉得架构应该叫做项目架构，是项目外面的组织方案。

后来，我觉得这应该是“设计模式”问题，可能我对设计模式的掌握不是很深入，应该再去理解、深挖前人的经验，从固定模式出发构建项目。在我花了好几天时间再次重新看了GOF的书、并做了一些详细的笔记之后（发现自己技术书籍的阅读速度也下降很多，注意力集中的时间减少了，如果现在的状态回归高中，肯定听不下来一节课），我发现其讨论的设计模式要更加微观一些，是在更细节的角度说明，如果你想摘除一些依赖应该怎样做。但是具体在一个项目中，什么位置用什么模式，仅仅做出了单独的举例，并没有给出一个通用项目搭建结构，而我准备对这方面给出一些思考过的成型方案。


### 编码之禅 zen for coding

Chapter 1. Let the IDE know you are doing. 让你的IDE知道你在干什么。

1. use identifiers as name rather than string. 标识符名优于字符串名。
