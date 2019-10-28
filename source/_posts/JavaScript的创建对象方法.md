---
title: JavaScript的創建方法
date: 2018-08-23 11:36:01
tags: JavaScript对象
categories: JavaScript
---
# JavaScript创建对象的几种方法
## 一、理解对象
ECMA-262把对象定义为： 无序属性的集合，其属性可以包含基本值，对象或者函数。每个对象都是基于一个引用
类型创建的，这个引用类型可以是原生类型，比如Object，Array等，也可以是自己定义的类型。<!--more-->
## 二、常用方法
### （1）创建单个对象
情景模式： 现在我们要创建一家公司的人员。
创建单个对象，也就是我们要创建一个人员。
####  a. 创建Object实例
	 传说女娲造人，Object其实可以想象成女娲，所有的对象都是Object的实例。
		var person = new Object();
		person.name = "zzilcc";
		person.age = 23;
		
new 其实做了四件事情。

	1. 创建了一个对象
	2. 把当前作用域赋值给这个对象
	3. 执行构造函数里的代码
	4. 返回这个对象
	
	但是我们更常用的方法是对象字面量方法。简单好理解。
####  b .对象字面量方法
	
	var person = {
		name: "bbb",
		age: 23,
		sayName: function(){
			console.log(this.name);
		}
	}
### (2) 创建多个对象


#### a. 工厂模式
此时，如果我们要创建多个人员，我们可能会这样写
	
		var person1 = new Object();
		person1.name = "aaa";
		person1.age = 23;
		person1.sayName = function(){
			console.log(this.name);
		};
		
		var person2 = new Object();
		person2.name = "bbb";
		person2.age = 23;
		person2.sayName = function(){
			console.log(this.name);
		};
		
		var person3 = new Object();
		person3.name = "ccc";
		person3.age = 23;
		person3.sayName = function(){
			console.log(this.name);
		};
		
		var person4 = new Object();
		person4.name = "ddd";
		person4.age = 23;
		person4.sayName = function(){
			console.log(this.name);
		};
		
这是我们会发现，我们写了大量重复的代码，能不能把相同代码放到一起，每次调用一下就好了，所以就有了工厂模式。

		function  createPerson (name,age) {
			var o = new Object();
			o.name = name;
			o.age = age;
			o.sayName = function(){
				console.log(this.name);
			}
		}
		var person1 = createPerson("aaa",23);
		var person2 = createPerson("bbb",21);
		var person3 = createPerson("ccc",24);
		var person4 = createPerson("ddd",22);
		
这样我们创建相似对象就可以减少重复代码量。但是这个方法有的缺点就是无法解决对象识别的问题。也就是通过工厂模式产生的对象只能知道是“女娲”（object）造出来的实例，他们之间不能细分到是这是男人还是女人。

#### b. 构造函数模式
这时候构造函数模式就可以解决对象识别的问题了。因为构造函数可以用来创建特定类型的对象。构造函数可以想象成女娲的各种法术，一种法术产生一种类型的人员，比如这种法术是生成“女性”，那种法术是生成“男性”。构造函数有原生构造函数和自定义的构造函数，非常人性化。

		function Male(name,age){
			this.sex = "male";
			this.name = name;
			this.age = age;
			this.sayName = function(){
				console.log(this.name)
			}
		}
		var male1 = Male("aa",23);
		var male2 = Male("xx",22);
		
按照惯例，构造函数的函数名首字母要大写。
我们可以通过instanceof操作符检测对象类型。使用构造函数意味着把它实例标识为一种特定的类型，比如男人，女人，老人，小孩等等。这也是工厂函数无法解决的问题。

		console.log(male1 instanceof Object); //true
		console.log(male2 instanceof Object); //true
		console.log(male1 instanceof Male); //true
		console.log(male1 instanceof Male); //true
		
male1,,male2是Object的实例，也是Male的实例。
		
但是这个方法也是有自己的缺点的，也就是每个方法都要在每个实例上重新创建一遍。
		
		function Male(name,age){
			this.sex = "male";
			this.name = name;
			this.age = age;
			this.sayName = function(){
				console.log(this.name)
			}
		}
也就是我们每次new Male()的时候，我们都要去重新创建一次sayName方法。
		因为函数也是一个对象，所以上面的函数我们可以改写成

	function Male(name,age){
			this.sex = "male";
			this.name = name;
			this.age = age;
			this.sayName = new Function("console.log(this.name)");
		}
	
也就是我们每次new Male()的时候我们都创建了一个Function的实例，那为什么我们不能在全局环境中创建一个，然后再Male函数里调用。

所以我们可以改写成下面这样：

	function Male(name,age){
			this.sex = "male";
			this.name = name;
			this.age = age;
			this.sayName = sayName;
		}
		function sayName(){
			console.log(this.name);
		}
	
但是这么干的话，其实也不合适，因为sayName函数明明是为你Male所用的，但是你却把它放到全局里，这不符合全局的概念。
而且要是构造很熟有很多函数的话，那么全局作用域就有很多“全局”函数，那样我们自定义的引用类型就没有封装性可言了。

#### c. 原型模式
我们创建的每个函数都有一个原型（prototype）属性,这个属性是一个指针，指向一个对象。这个对象包含了一些属性和方法，这些属性和方法是被特定类型的所有实例共享的。也就是说prototype是我们通过构造函数创建的对象实例的原型对象。也就是我们把想要所有对象实例都共享的方法和实行都添加到原型中，而不是构造函数中。

		funtiton Person(){};
		Person.prototype.name = "aa";
		Person.prototype.age = 23;
		Person.sayName.sayName = function() {
			console.log(this.name)
		}
		
		var person1 = new Person();
		person1.sayName();//"aa"

我们把公用属性和方法放到了Person的原型中， 所以每个实例访问的都是同一组属性和同一个方法。这样就不用把方法放到全局环境去写了，就解决了构造函数把私有方法放到全局的问题

#### d. 组合使用构造函数+原型模式

俗话说，我们要去其糟粕，取其精华，我们将两种方式的精华合并到一起，集两家之长，形成了组合模式。使用构造函数模式定义实例属性，用原型模式定义方法和共享的属性。

	function Peroson (name, age) {
		this.name = name;
		this.age = age;
		this.friends = ['zz', 'aa'];
	}
	
	Person.prototype = {
		constructor: Person,
		sayName: function () {
			console.log(this.name)
		}
	}
	
	var person1 = new Person('zzilcc', 23);
	var person2 = new Person('aaa', 22);
	