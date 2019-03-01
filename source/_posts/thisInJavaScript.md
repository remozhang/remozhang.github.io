---
title: JavaScript中的this
date: 2017-01-02 20:37:00
tags: JavaScript
cdn: 'header-on'
header-img: 'large/6996c260ly1g0l1do94olj208b04o3yh.jpg'
---

## 前言

javascript中的this到底是个什么东西？表示学了这么久有时候还是会出现混淆，她简直像个恶魔！
群里大神一句话说过是指向直接调用她的对象，也就是点前的对象，我研究了下，终是有所领悟。
<center>![JavaScript中的this](https://wx1.sinaimg.cn/large/6996c260ly1g0l1do94olj208b04o3yh.jpg)</center>


## 她是个啥？
首先，`this`是javascript语言的关键字之一，指函数运行时的当前对象，那既然和函数运行有关，js中函数有哪些调用模式呢？

`1.纯粹的函数调用`
`2.对象的方法调用`
`3.构造函数的调用`
`4.apply、call调用`

来来来，让我来一步一步解开她的衣衫
<center>![老司机](https://wx2.sinaimg.cn/large/6996c260ly1g0l1ds9ucfj20b406yaal.jpg)</center>
<!-- more -->

## 1.纯粹的函数调用

**函数调用 即`function name()`模式，这也是我们使用的最多的一种方式，其属于全局调用，浏览中的默认情况下函数内部的this指向`window`，当然是在非严格模式下。**

```javascript
this.name = 'remo';
function showName() {
	console.log(this.name);
	console.log(this === window);
}
showName()

//remo
//true
```
上面的例子相当于

```javascript
widow.showName()
```

这也是为什么可以读取到全局定义的`name`属性的原因。

## 2.对象的方法调用

当一个函数作为对象的某个属性方法被调用的时候

```javascript
var obj = {
	name: 'remo',
	showName: function() {
		console.log(this.name);
	}
};

obj.showName();
//remo
```

**可以看出`this`指向的是`obj`这个对象，其实本质上讲函数调用形式内部`this`就是指向调用它的那个对象。**

**`再来`**

```javascript
var showName = function() {
	console.log(this.name);
}

obj = {
	name: 'remo',
	showName: showName
};

obj.showName();
//remo
```

结果是不变的，在js中，一切都是对象，而这里也只是， 将`obj`的`showName`属性指向，`showName`函数的引用地址。

**`继续`**

当我们把`showName`方法赋值给一个变量，又会有什么事情发生呢？

```javascript
var obj = {
	name: 'remo',
	showName: function() {
		console.log(this.name);
	}
};

var tempShowName = obj.showName;

tempShowName()

//undefined
```

为什么不是期望的那样输出remo呢。`obj`的`showName`方法是一个对象，当把它赋值给了`tempShowName`变量，此时便和`obj`没什么关系了，也就是和下面的等价了

```javascript
window.tempShowName()
```

window上此事并没有`name`属性，输出自然是`undefined`。


## 3.构造函数调用

当使用`new`去调用一个构造函数的时候，内部的this，指向的是实例化出来的对象。

```javascript
var Person = function (name, sex) {
    this.name = name;
    this.sex = sex;
    console.log(this);
};

var p1 = new Person('remo', 'boy');

// Person {name: 'remo', sex: 'boy'};
```

构造函数也是函数，所以当你用普通调用方式调用时

```javascript
var Person = function (name, sex) {
    this.name = name;
    this.sex = sex;
    console.log(this);
};

Person('remo', 'boy');
//这个时候相当于给window对象添加了name和sex两个属性。

window.name // 'remo'
window.sex // 'boy'
```

## 4.apply、call方法调用

使用`call`和`apply`方式去调用一个函数的时候，内部的this指向的是传进来的第一个参数，当第一个参数是`undefined`或者`null`的时候，依旧指向`window`

```javascript
var showName = function() {
	console.log(this);
}

showName();//window
showName.call(undefined);//window
showName.call(null);//window
showName.call(remo);//remo
```

## 5.箭头函数

在ES6中的新规范中，加入了箭头函数，它比普通函数方便，清晰了许多，但关于`this`的指向，普通函数的`this`是运行时候决定的，而箭头函数则是定义的时候就决定的了，它内部本身是不包含`this`的。

```javascript
var obj = {
	name: 'remo',
	showName: function() {
		console.log(this.name);
	},

	showNameLater: function() {
		setTimeout(()=>{
			console.log(this.name);
		},1000)
	}
};

obj.showNameLater();

//remo
```

```javascript
var obj = {
	name:'remo',
	showName: () => {
		console.log(this.name);
	}
};

obj.showName();
//undefined
```

## 最后
文章有疏漏与错误之处，望指出！