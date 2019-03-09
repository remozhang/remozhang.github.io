---
title: PHP 基础闭坑指南一:执行原理和流程
tags: PHP 基础闭坑指南
date: 2017-07-07 16:37:00
toc: true
---
# PHP 执行流程图
<center>![PHP 执行流程图](http://wx2.sinaimg.cn/large/6996c260ly1g0t3txek6lj20ry0h8q47.jpg)</center>
<!-- more -->

# PHP 启动流程说明
## PHP 启动第一步: 初始化各个模块
PHP 调用各个扩展的 `MINIT` 方法, 从而使这些扩展切换到可用状态
可以在 `php.ini` 查看 PHP 都打开了哪些模块
## PHP 启动第二部: 请求初始化
当一个页面请求发生时, SAPI 层将控制权交给 PHP 层, 于是 PHP 设置了用于回复本次请求所需的环境变量.同时, 它还建立一个变量表, 用来存放执行过程中产生的变量名和值
PHP 调用各个模块的 `RINIT` 方法, 即"请求初始化".一个经典的例子是
```$xslt
	Session模块的 RINIT, 如果在 php.ini 中启用了 Session模块, 那在调用该模块的 RINIT 时就会初始化$_SESSION变量, 并将相关内容读入.
```
`RINIT` 方法可以看作是一个准备的过程, 在程序执行之前就会启动.



# PHP 关闭流程说明
## PHP 关闭第一步: 清理程序
一旦页面执行完毕(无论是执行到了文件末尾还是用 `exit` 或者 `die` 函数终止) PHP 就会清理程序. 它会按顺序调用各个模块的 `RSHUTDOWN` 方法.
`RSHOTDOWN` 用以清除程序运行时产生的符号表, 也就是对每个变量调用 `unset` 函数.

## PHP 关闭第二步:  关闭各个模块
PHP 调用每个扩展的 `MSHOTDOWN` 方法, 这是各个模块最后一次释放内存的机会.
这样, 整个 PHP 生命周期就结束了. 要注意是, 只有在服务器没有请求的情况下才会执行 "启动第一步" 和 "关闭第二步".

# PHP 底层原理
<center>![PHP 执行底层原理](https://wx3.sinaimg.cn/mw690/6996c260ly1g0t4q4tvtmj20ea0el75n.jpg)</center>
## 四层体系
`1.Zend 引擎`
`2.Extensions`
`3.SAPI`
`4.上层应用`
## Zend引擎
Zend 整体是用C语言实现的, 是PHP内核部分. 它将 php 代码翻译（词法、语法解析等一系列编译过程）为可执行 opcode 的处理并实现相应的处理方法。实现了基本的数据结构（如hashtable、oo）、内存分配及管理、提供了相应的 api 方法供外部调用。是一切的核心，所有的外围功能均围绕 zend 实现。 
## Extensions
围绕着 zend 引擎，extensions 通过组件式的方式提供各种基础服务.我们常见的各种内置函数（如array系列）、标准库等都是通过extension来实现。用户也可以根据需要实现自己的 extension 以达到功能扩展、性能优化等目的。
## SAPI
SAPI 全称是 Server Application Programming Interface，也就是服务端应用编程接口。SAPI 通过一系列钩子函数，使得 php 可以和外围交互数据，这是 php 非常优雅和成功的一个设计。通过 SAPI 成功的将 php 本身和上层应用解耦隔离，php 可以不再考虑如何针对不同应用进行兼容，而应用本身也可以针对自己的特点实现不同的处理方式。
## 应用层
这就是我们平时编写的 php 程序，通过不同的 SAPI 方式得到各种各样的应用模式，如通过 webserver 实现 web 应用、在命令行下以脚本方式运行等等。

# 相关资料
[http://www.php-internals.com/](http://www.php-internals.com/)

[http://blog.csdn.net/qq_28602957/article/details/53363963
](http://blog.csdn.net/qq_28602957/article/details/53363963
)

