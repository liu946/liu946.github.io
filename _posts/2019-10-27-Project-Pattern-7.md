---
layout: plain
title: 项目模式（七）—— 日志系统
category: tech
---

### 附加功能

1. 同时向命令行和文件输出日志（也可以尝试用 tee 指令完成）
2. 动态增加和修改输出到的日志文件
3. 自动打包
4. Optional: 颜色


### 关于日志使用

1. 日志级别，error，会导致5xx的错误，程序只能崩溃掉（由于服务框架，程序不会崩掉，因此这个日志也是必要的）
2. 日志级别，warning，可能导致错误，或者处理已经预知的错误，只能降级提供服务的
3. 日志级别，info，提升程序运行的阶段，尽量不要在循环中使用。尽量保证一次执行，相同位置的info日志仅报告一次。http请求与返回例外。
4. 日志级别，debug，可以在循环中设置，尽可能详细的报告运转信息，尤其是在有随机逻辑的位置。
5. 日志与进度条：进度条不是日志，进度条请使用标准流输出实现，不要和日志打印在一个流中。进度条走完之后，可以在日志中输出一个综合的信息来报告处理完成以及时间等等信息。

### 关于日志的头内容讨论

这里讨论每条日志打印时的头信息最好包含哪些字段。因为每条日志都会输出，这里是寸土寸金的，尽量少输出，输出重要信息。分两种情况：

1. 服务器日志（代码已经成型，错误很少，日志主要目的是为了记录和分析数据）

- 时间（精确到秒即可，不需要使用星期，推荐的format string "%Y-%m-%d %H:%M:%S" ）
- 日志级别（使用首字母即可）

2. 调试日志（代码还在修改之中，其中debug日志很多，主要目的是测试查看是否会有地方触发bug）

- 时间（同1）
- 日志级别（同1）
- 日志报告位置信息（哪个文件，第几行报告这个日志）
- 
