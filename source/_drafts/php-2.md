---
title: PHP 基础闭坑指南二:常量
tags: PHP 基础闭坑指南
date: 2017-07-14 13:37:00
toc: true
---
# PHP 常量脑图
<center>![PHP 常量](https://wx4.sinaimg.cn/mw690/6996c260ly1g0v799ek1nj20tq12t0x0.jpg)</center>
<center>[🙋看不清图片的点这里](https://wx4.sinaimg.cn/mw690/6996c260ly1g0v799ek1nj20tq12t0x0.jpg)</center>
<!-- more -->

# 什么是常量
常量是一个简单值的名称或者标识

# 常量的特征
1. PHP 代码运行期间不能修改常量的值(除了魔法常量, 那不算是真正意义上的常量)
2. 大小写敏感, 为了方便, 通常大写
3. 常量只能是标量(boolean, integer, float and string), PHP5.6之后可以定义为标量表达式或者是一个数组

# 常量和变量之间的区别
## 定义
定义变量使用$符开始
定义常量不需要$符号开始
## 赋值
变量支持赋值操作
常量不支持赋值操作
## 值
可以改变变量的值
不可以改变常量的值
## 作用域
变量有作用域
常量没有作用域,在代码任何地方都可以访问常量

# 常量命名规则
第一个字符必须是字母或者下划线'\_'
第二个以及后续字母可以包含字符, 数字或者下划线'\_'

# 常量定义方法
define("常量名称", 值)
const 关键词 注意事项: 和使用 define() 来定义常量相反的是, 使用 const 关键字定义常量必须处于最顶端的作用域, 因为用此方法是在编译时定义的, 这就意味着不能在函数内, 循环内以及 if 语句之内用 const 来定义常量

# const 和 define() 的区别
## 定义常量时机
const 编译代码时
define() 执行代码时
## 条件语句中定义
const 不支持
define 支持
## 常量名称
const 只能是普通的常数
define() 可以是普通的常数, 也可以是表达式
## 常量名称大小写敏感性
const 大小写敏感
define() 可以大小写不敏感

# 获取常量值的方法
1. 直接使用常量名称
2. constant("常量名称")

# 魔术常量
\__LINE\__ : 文件里\__LINE\__所在行的行号
\__FILE\__: \__FILE\__所在文件的文件全路径
\__FUNCTION\__: \__FUNCTION\__常量所处作用域的函数名称
\__DIR\__: 当前代码文件的目录
\__TRAIT\__: 返回 trait 被定义时的名字
\__CLASS\__: \__CLASS\__常量所在位置的类名称
\__METHOD\__: \__METHOD\__常量所在位置的类方法名称
\__NAMESPACE\__:  当前命名空间的名称

# 相关资料
[https://phpbestpractices.org/#constants](https://phpbestpractices.org/#constants)
[https://stackoverflow.com/questions/2447791/define-vs-const/3193704#3193704](https://stackoverflow.com/questions/2447791/define-vs-const/3193704#3193704)




