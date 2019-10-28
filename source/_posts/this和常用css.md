---
title: this和常用css
date: 2019-04-26 09:44:50
tags: this | css
---
## this

### 第一段代码

	var count = 1;
    function a () {
        this.count ++
        console.log(this.count)
    }
    a.count = 0;
    a()
    console.log(a.count)
   
谣言： this指向自身



### 第二段代码

重要的事情说三遍

this永远指向最后调用它的对象

this永远指向最后调用它的对象

this永远指向最后调用它的对象
<!--more-->

    var name = 'windowName';
    function a () {
        var name = 'aName';
        console.log('a: ' + this.name)
    }
    a()
    console.log('window: ' + this.name)

输出？

两个都是输出windowName，因为a函数在全局对象里调用的，所以this指向的是window，所以第一个代码a函数里this.count++,这个count是全局的coount，也就是window.count,a.count不会变,所以输出的是2，0。然后第二段代码两个输出都是windowName

### 第三段代码

	var name = 'windowName';
	function a () {
		var name = 'aName';
		console.log('a: ' + this.name);
	}
	var obj = {
		name: 'objName',
		fn: a
	}
	obj.fn()
	
输出？
	
因为最后调用this的对象是obj，所以this指向obj，this.name指的是obj.name
	
### 第四段代码

    var name = 'windowName';
    function a () {
        var name = 'aName';
        console.log('a: ' + this.name);
        function b() {
        	console.log('b: ' + this.name)
    	 }
    	 b();
    }
    a()
    console.log('window: ' + this.name)
    
输出？

在js里，函数是一种特殊的对象，只要函数里没有被正常对象包裹着，函数调用this都是指向window。

所以这里输出都是windowName

### 第五段代码

	var name = 'windowName';
	function a () {
		var name = 'aName';
		console.log('a: ' + this.name);
	}
	var obj = {
		name: 'objName',
		fn: a
	}
	var foo =  obj.fn 
	foo()
	
这里我们变形一下第三段代码，将obj.fn赋值给一个变量foo，然后再运行foo，这样会输出什么？

很神奇，这里会输出的是‘windowName’,而不是‘objName’，这是因为把obj.fn赋值给foo时，是相当于foo指向了fn函数，然后foo时再全局执行的，所以相当于window.foo,所以this指向是window，所以输出的是‘windowName’。

### 第六段代码

	var name = 'windowName';
	setTimeout(function(){
		var name = 'setTimeout_name'
		console.log(this.name)
	},1000)
	
我们之前说过setTimeout是window的方法，setTimeout的回调函数是在window里执行的，所以setTimeout回调函数里的this指向的是window。

### 总结：

this永远指向最后调用它的对象

this永远指向最后调用它的对象

this永远指向最后调用它的对象

## 改变this指向

1. 使用es6的箭头函数
2. 在函数内部使用_this = this
3. 使用apply，call，bind
4. new实例话一个对象。 

### es6的箭头函数

es6的箭头函数的this始终指向的是函数定义时的this，而非执行时。

	var name = 'windowName';
	var obj = {
		name: 'objName',
		fn: function() {
			setTimeout(()=>{
				console.log(this.name)
			},0)
		}
	}
	obj.fn()
 
### _this,that,self

这种方法最常见了，用一个变量_this,that,self保存一下调用这个函数的对象，然后在函数里用这个变量

	var name = 'windowName';
	var obj = {
		name: 'objName',
		fn: function() {
			var _this = this;
			setTimeout(function(){
				console.log(_this.name)
			},0)
		}
	}
	obj.fn()

### call,apply,bind

	var name = 'window_name'
	var a = {
		name: 'a_name',
		fn: function(age){
			console.log(this.name);
		}
	}
	var b = {
		name: 'b_name',
		fn1: function(){
			console.log(this.name);
		}
	}
	a.fn.apply(b)
	b.fn1.apply(a)
	b.fn1.apply(this)
	
	a.fn.call(b)
	b.fn1.call(a)
	b.fn1.call(this)
	
	a.fn.bind(b)()
	b.fn1.bind(a)()
	b.fn1.bind(this)()
	
apply 语法 fun.apply(thisArg, [argsArr])

* thisArg fun函数运行时指定的this值
* argsArr 一个数组或者类数组对象。

call 语法 fun.call(thisArgs, arg1, arg2...)

apply和call的区别是call是接受多个参数，apply接受一个参数数组
  
	var a = {
		name: 'a_name',
		fn: function(age, sex){
			debugger
			var age = age;var sex = sex;
			console.log(this.name);
		}
	}
	var b = {
		name: 'b_name',
		fn1: function(age, sex){
			debugger
			console.log(this.name);
		}
	}
	a.fn.apply(b,[ 11, 'man'])
	
	b.fn1.call(b,  11, 'man')
	
### new

我们经常说没有对象，new一个就行。这里的new将this指向

	var Person (name) {
		this.name = name
	}
	
	new Person('zzilcc')

new 做了什么，下面解释一下

1. 创建了一个空对象obj
2. 把obj的_proto_z指向Person的原型对象prototype，此时便建立了obj对象的原型链obj->Person.prototype->Object.prototype->null
3. 在obj的执行环境调用Person的方法，也就是Person.call(obj,'zzilcc'),然后执行obj.name = 'zzilcc'
4. 将obj当作返回值返回

所以我们用一个变量去接受下这个obj

	var person1 = new Person('zzilcc')
	person1.name === 'zzilcc' // true


## 常用css属性

1. css背景属性

    * background: #fff url() center 100% no-repeat
        * background-color
        * background-image
        * background-position
        * background-size
        * background-repeat

2. css边框属性

    * border
        * border-color
        * border-width
        * border-style
    * border-top: 1px solid #fff
        * border-top-color: #fff
        * border-top-width: 1px
        * border-top-style: solid(实线)/dotted(点状)/dashed(虚线)
    * border-right
        * border-right-color
        * border-right-width
        * border-right-style
    * border-bottom
        * border-bottom-color
        * border-bottom-width
        * border-bottom-style
    * border-left
        * border-left-color
        * border-left-width
        * border-left-style

3. css尺寸属性

    * height
    * max-height
    * min-height
    * width
    * min-width
    * max-width

4. css字体属性

    * font
        * font-size
        * font-family
        * font-style
        * font-weight

5. css外边距属性

    * margin
        * margin-top
        * margin-right
        * margin-bottom
        * margin-left

6. css内边距属性

    * padding
        * padding-top
        * padding-right
        * padding-bottom
        * padding-left

7. css定位属性
    * position
    * top
    * right
    * bottom
    * left
    * overflow
    * float
    * display
    * z-index
    * vertical-align
    * cursor: default|pointer

8. css文本属性

    * color: #fff; // 颜色
    * line-height:40px; //行高 
    * text-align: left|center|right// 规定文本的水平对齐方式
    * text-indent: 2px|1% // 属性规定文本块中首行文本的缩进。
    * white-space:nowrap // 	文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止
    * text-overflow:ellipsis // 规定当文本溢出包含元素时发生的事情。
    * word-break: normal|break-all|keep-all;// 规定非中日韩文本的换行规则。
    * word-wrap: normal|break-word // 单词分割且换行



## 常用css解决某些问题

1. css画各种形状

### 圆形

	div {
		width: 100px;
		height: 100px;
		background: red;
		border-radius: 50%;
	}
	
	<div></div>
	
### 三角形

	div {
		  width: 0;
		  border-left: 50px solid transparent;
		  border-right: 50px solid transparent;
		  border-bottom: 100px solid red;
	}

2. 省略号
### 省略号
		
		max-width: 100px;
		overflow:hidden;
    	text-overflow:ellipsis;
    	white-space:nowrap
    
## 绑定数据

## 彩蛋

git reflog && git reset --hard '哈希数'

遇到一些奇怪的现象时我们可以用git reflog 找到我们最新的一次commit时的哈希数。

然后灭霸一个响指可以消灭一半的‘人’

我们git reset --hard ‘哈希数’则能让我们回到刚刚commit完的时候，仿佛之前进行了一切操作犹如云烟飘散。