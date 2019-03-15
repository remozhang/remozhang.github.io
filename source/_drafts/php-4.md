---
title: PHP 基础闭坑指南四:PHP类型
tags: PHP 基础闭坑指南
date: 2017-07-30 13:37:00
toc: true
---
# PHP 类型脑图
<center>![PHP 类型](https://wx1.sinaimg.cn/mw690/6996c260ly1g12bbx30ssj21682x17ik.jpg)</center>
<center>[🙋看不清图片的点这里](https://wx1.sinaimg.cn/mw690/6996c260ly1g12bbx30ssj21682x17ik.jpg)</center>
<!-- more -->

# PHP 类型分类
PHP 支持9种原始数据类型
1. 四种标量类型:
	+ boolean 布尔型
	+ integer 整形
	+ float 浮点型, 也称作double, 这里涉及精度概念[详见](https://floating-point-gui.de/)
	+ string 字符串 (PHP 每个字符等于一个字节, 只能支持256的字符集, 因此不支持Unicode)

2. 三种复合类型:
	+ array 数组
	+ object 对象
	+ callable 可调用 
	
3. 最后是两种特殊类型:
	+ resource 资源
	+ NULL 无类型

变量的类型通常不是由程序员设定的, 确切地说, 是由 PHP 根据该变量使用的上下文在运行时决定的
