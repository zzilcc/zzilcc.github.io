---
title: JavaScript数据结构
date: 2019-07-27 14:26:30
tags: javaScript
categories: 数据结构
---
## 前言

想要做一个技术人，数据结构和算法都是必须的，在大学中，最让我头疼的也是这两门课，总觉得脑豁疼，毕业工作后一直想要找时间学习，但是奈何在前公司总是搬砖，做一些简单的工作，现离职后开始找工作，终于抽出时间开始学习数据结构和算法。数据结构和算法对我来说是难以翻越两座大山，但是做人要不断挑战自己，这一篇博客主要是记录一下学习数据结构的成果。

数据结构按可以分为逻辑结构和物理结构。把数据结构比作人的话，物理结构就是看得见，摸得着的人体，逻辑结构就是人的精神和思想。

物理结构分为顺序存储结构和链式存储结构。顺序存储结构有数组，链式存储结构有链表。

逻辑结构分为线性结构和非线性结构。线性结构主要有顺序表，栈，队列。非线性结构主要有树，图。

<!--more-->

## 物理结构

### 顺序存储结构

顺序存储结构顾名思义就是数据在内存中是顺序存储。

#### 数组

数组是最简单的数据结构，它一般来说存储着有限个相同类型的变量，在js中，数组可以保存着不同类型的值，但是不推荐这么用。

我们知道，内存是由一个个连续的内存单元组成，数组中的每个元素都连续存储在内存中，而且是顺序存储。

##### 创建和初始化数组

创建和初始化数组有三种方式，一种是通过构造函数，一种是字面量，最后一种是Array.of()。

第一种： 

```js
let arr = new Array(10) // 创建一个空数组，数组长度为10
let arr1 = new Array('10') // 创建了一个数组['10'],数组长度为1
let arr2 = new Array('10','11') // 创建了一个数组['10,11'],长度为2
```

我们可以看到通过构造函数创建数组时，如果向构造函数传递了一个Number类型的参数，那么会生成一个length为传进来的参数的大小，否则则生成一个包含参数的数组。

第二种：


```js
let arr = [] // 创建一个空数组，数组长度为0
let arr1 = ['10'] // 创建了一个数组['10'],数组长度为1
let arr2 = ['10,11'] // 创建了一个数组['10,11'],长度为2
```

第二种方法是字面量方法，直接通过‘[]’创建数组。

第三种是新增的方法

```js
let arr = Array.of() // 创建一个空数组，数组长度为0
let arr1 = Array.of('10') // 创建了一个数组['10'],数组长度为1
let arr2 = Array.of('10','11') // 创建了一个数组['10,11'],长度为2
```

##### 访问元素

我们通过元素下标访问元素数组。数组第一个元素的下标为0，最后一个为length-1。


##### 添加和删除数组元素

###### 添加元素到数组首位--unshift()

语法： arrayObject.unshift(item)

参数： item： 要插入到首位的元素

```js
let arr = [1,2,3];
arr.unshift(0)
console.log(arr)// [0, 1, 2, 3]
```
######  删除数组首位元素--shift()

语法： arrayObject.shift()


```js
let arr = [1,2,3];
arr.shift()
console.log(arr)// [2, 3]
```

######  添加元素到数组末尾--push()

语法： arrayObject.push(item)

参数： item： 要插入到末位的元素

```js
let arr = [1,2,3];
arr.push(4)
console.log(arr)// [1, 2, 3, 4]
```

####### 删除数组末尾元素--pop()

语法： arrayObject.pop()


```js
let arr = [1,2,3];
arr.pop()
console.log(arr)// [1, 2]
```

###### 添加/删除元素到数组任意位置--splice()

语法： arrayObject.splice(index,howmany,item1,.....,itemX)

参数： 

1. index：必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
2. howmany：必需。要删除的项目数量。如果设置为 0，则不会删除项目。
3. item1,.....,itemX：可选。向数组添加的新项目。
	

```js
let arr = [1,2,3];
arr.splice(1, 0, 5, 5)
console.log(arr)// [1, 5, 5, 2, 3]
```

##### 数组方法

上面我们已经接触了5个方法了。下面将介绍一下数组的其他的方法。

###### concat 连接数组

连接两个及以上的数组，并返回一个新数组，不会影响旧数组

```js
let arr = [1, 2, 3];
let arr2 = [3, 4, 5];
var res = arr.concat(arr2);
console.log(res)// [1, 2, 3, 3, 4, 5]
```

###### every 返回值是boolean

对数组中的每个元素运行一个函数，如果每个元素运行该函数返回为true，则为true。

```js
let arr = [1, 2, 3];
var res = arr.every(function (item, index, arrObj) {
	return item > 0
});
console.log(res)// true
```

该函数接收三个参数，item是当前元素，index是该元素的下标，arrObj是执行every方法的数组。

###### some 返回值是boolean

对数组中的每个元素运行一个函数，如果每个元素运行该函数有一个返回为true，则为true。


```js
let arr = [1, 2, 3];
var res = arr.some(function (item, index, arrObj) {
	return item > 2
});
console.log(res)// true
```

###### map 返回新数组

对数组中的每个元素运行一个函数，每次调用该函数的结果组成新数组返回

```js
let arr = [1, 2, 3];
var res = arr.map(function (item, index, arrObj) {
	return item * 2
});
console.log(res)// [2, 4, 6]
```

###### filter 过滤元素，返回新数组

对数组中的每个元素运行一个函数，每次调用该函数的返回值为true的元素组成新数组返回

```js
let arr = [1, 2, 3];
var res = arr.filter(function (item, index, arrObj) {
	return item > 2
});
console.log(res)// [3]
```

###### forEach 无返回值

对数组中的每个元素运行一个函。


```js
let arr = [1, 2, 3];
arr.forEach(function(){
	// 某些操作
});
```

###### slice 截取数组，返回新数组

传入索引值(start, end)，将数组里对应索引范围内(包含start，不包含end)的元素组成新数组返回

```js
let arr = [1, 2, 3];
var res = arr.slice(0, 1);
console.log(res)// [1]
```

###### sort 排序数组，影响arr数组

按照字母顺序对数组排序，支持指定的排序函数当作参数

```js
let arr = [2, 3, 4, 1, 2, 3];
var res = arr.sort();
console.log(res)// [1, 2, 2, 3, 3, 4]
```

###### reverse 颠倒数组，影响arr数组

颠倒数组，原先第一位元素变成最后一位，第二位变成倒数第二位，以此类推。

```js
let arr = [1, 2, 3];
var res = arr.reverse();
console.log(res)// [3, 2, 1]
```

###### indexOf 返回第一个与给定参数相等的元素的下标，没有返回-1

从数组的第一个元素开始匹配，匹配成功则返回下标

```js
let arr = [1, 2, 3];
var res = arr.indexOf(2);
console.log(res)// 1
```

###### lastIndexOf

从数组的最后一个元素开始匹配，匹配成功则返回下标，没有匹配成功返回-1

```js
let arr = [1, 2, 3, 2];
var res = arr.lastIndexOf(2);
console.log(res)// 3
```

###### join 将所有元素拼接成字符串


```js
let arr = [1, 2, 3];
var res = arr.join();
console.log(res)// "1,2,3"
```

###### toString 将所有元素拼接成字符串


```js
let arr = [1, 2, 3];
var res = arr.toString();
console.log(res)// "1,2,3"
```

###### reduce 累加

reduce对元素的每一项运行一个函数，这个函数接收四个参数，preV前一个元素的值，curV当前元素值，index当前元素的下标，arrObj，执行reduce函数的数组。

reduce会返回数组每一项的累加值。

```js
let arr = [1, 2, 3];
var res = arr.reduce(function(preV, curV, index, arrObj){
	return preV + curV
});
console.log(res)//6  1+2+3=6
```

###### copyWithin 复制数组的某个范围的元素到同一个数组指定的起始位置


```js
let arr = [1, 2, 3];
var res = arr.copyWithin(1, 0, 1);
console.log(res)// [1, 1, 3]
```

copyWithin接收三个参数，第一个参数值指定元素放的起始位置，第二个，第三个参数分别是复制元素的起始位置和结束位置。

复制的元素包括开始位置的元素，不包括结束位置的元素。

###### entries 返回包含数组所有键值对的 @@iterator


```js
let arr = [1, 2, 3];
var res = arr.entries();
console.log(res.next().value)// [0, 1] 0是下标，1时该下标对应的元素
```


###### includes 检测数组是否包含某个值


```js
let arr = [1, 2, 3];
var res = arr.include(1);
console.log(res)// true
```


###### find 数组每一项运行一个给定的函数，如果运行返回true，则返回这个元素


```js
let arr = [1, 2, 3];
var res = arr.find(function(item){
	return item > 1
});
console.log(res)// 2
```


###### findIndex 数组每一项运行一个给定的函数，如果运行返回true，则返回这个元素的下标


```js
let arr = [1, 2, 3];
var res = arr.findIndex(function(){
	return item > 1
});
console.log(res)// 1
```

###### fill 用静态值填充数组

fill函数接收三个参数，填充值（必须），开始位置，结束位置


```js
let arr = [1, 2, 3];
var res = arr.fill(2, 0, 1);
console.log(res)// [2, 3, 3]
```


###### from 从一个类似数组或可迭代对象中创建一个新的，浅拷贝的数组实例


```js
Array.from("foo");//['f', 'o', 'o']
```

Array.from这个方法接收三个参数，第一个是要转换成数组的类数组对象，第二个是新数组的每一项都会运行的函数，第三个参数this

```js
var res = Array.from([1, 2, 3], x => x*2);//[2, 4, 6]
```
###### values 包含数组所有值的@@iterator


```js
let arr = [1, 2, 3];
let res = arr.values().next().value // 1
arr.values().next().value // 2
```


###### key 包含数组所有下标的@@iterator


```js
let arr = [1, 2, 3];
let res = arr.keys().next().value // 0
arr.values().next().value // 1
```

###### flat 降维数组


```js
let arr = [1, [2, [3, [4, 5]]], 3];
arr.flat(1) // [1, 2, [3, [4, 5]], 3]
arr.flat(2) // [1, 2, 3, [4, 5], 3]
arr.flat(3) // [1, 2, 3, 4, 5, 3]
```

flat函数接收一个参数，要提取嵌套数组的结构深度，默认值为 1。

###### flatMap 包含数组所有下标的@@iterator

它与 map 和 深度值1的 flat 几乎相同

```js
let arr1 = [1, 2, 3, 4];
arr1.map(x => [x * 2]); 
// [[2], [4], [6], [8]]
arr1.flatMap(x => [x * 2]);
// [2, 4, 6, 8]
// 只会将 flatMap 中的函数返回的数组 “压平” 一层
arr1.flatMap(x => [[x * 2]]);
// [[2], [4], [6], [8]]
```



### 链式储存结构

数组的大小是固定，我们向数组的首部或者中间插入或者删除元素的成本很高，因为要移动元素。链式存储结构就很好的解决了这个问题，因为链式存储结构的元素不是连续存放在内存中。

#### 链表

链表就是一种很常见的链式存储结构，链表中的每个元素由一个存储数据的节点和指向下一个元素的指针。因此向链表中添加和删除元素是速度很快的，只要改变一下元素的指向，而不需要移动元素。

下面我们用js去实现一个链表结构

```js
function LinkList () {
	let node = function (el) {
		this.el = el;
		this.next = null;
	};
	let length = 0;
	let head = 0;
	// 链表的常用操作
	this.append = function (el) {}; // 向链表尾部添加新的元素
	this.insert = function (position, el) {}; // 向链表的特定的位置添加一个元素
	this.removeAt = function (position) {}; // 删掉指定位置的元素
	this.remove = function (el) {}; // 删除元素
	this.indexOf = function (el) {}; //返回指定元素的索引，没有这返回-1
	this.isEmpty = function () {}; // 判断是否是空链表
	this.size = function () {}; //  返回链表长度
	this.getHead = function () {}; // 返回链表头部
	this.toString = function () {}; // 输出元素值
	this.print = function () {}; // 输出链表元素
}
```



## 逻辑结构

### 线性结构

#### 栈

栈是一个有序集合，并且遵循着先进后出，后进先出的原则。元素出去或者是进来的地方叫做栈顶，另一端是栈底。

下面上代码

```js
function Stack () {
	let items = [];
	this.push = function (element) { // 添加一个元素
		items.push(element);
	}; 
	this.pop = function () { // 移除栈顶的元素，同时返回被移除的元素
		items.pop();
	}; 
	this.isEmpty = function () { // 判断栈是否空，为空返回true，否则返回false
		if(items.length > 0) {
			return true;
		} else {
			return false;
		}
	}; 
	this.clear = function () { // 移除栈里的元素
		items = []
	}; 
	this.size = function () { // 返回栈的元素个数。
		return items.length;
	}; 
	this.print = function () { // 输出栈
		return items
	}
}
```

#### 队列

队列是一组有序的项，遵守先进先出，后进后出的原则。比较常见的例子是打印机的打印队列，先发起的打印请求肯定先打印，后发起的请求后打印。

```js
function Queue () {
	let items = [];
	this.enqueue = function (element) { // 添加一个元素
		items.push(element);
	}; 
	this.dequeue = function () { // 移除队列头部的元素，同时返回被移除的元素
		items.shift();
	}; 
	this.isEmpty = function () { // 判断队列是否空，为空返回true，否则返回false
		if(items.length > 0) {
			return true;
		} else {
			return false;
		}
	}; 
	this.clear = function () { // 移除队列里的元素
		items = []
	}; 
	this.size = function () { // 返回队列的元素个数。
		return items.length;
	}; 
	this.print = function () { // 输出队列
		return items
	}
}
```

### 非线性结构

#### 树

#### 图


