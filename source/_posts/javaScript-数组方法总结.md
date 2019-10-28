---
title: javaScript 数组方法总结
date: 2019-06-15 11:14:08
tags: JavaScript Array
---
## 数组方法总结
### 1. concat()

```	
语法： arr1.concat(arrayX,arrayX,......,arrayX)
返回值：一个连接新数组，包含了arr1和所有arrayX
参数：arrayX：可以是具体元素值，也可以是数组，数量是任意
作用：连接两个或多个数组
缺点：效率低

```

示例1：

```javaScript
let arr1 = [1, 2, 3];
let resArr = arr1.concat(4, 5)
console.log(resArr);// [1, 2, 3, 4, 5] 
```
<!--more-->
示例2:


```javaScript
let arr1 = [1, 2, 3];
let resArr = arr1.concat([4, 5])
console.log(resArr);// [1, 2, 3, 4, 5] 
```


示例3:


```javaScript
let arr1 = [1, 2, 3];
let resArr = arr1.concat([4, 5],[6, 7, 8])
console.log(resArr);// [1, 2, 3, 4, 5, 6, 7, 8] 
```


### 2. Array()
```	
语法： new Array(xArrayElement)
返回值： 一个Array实例
参数：xArrayElement数组里的内容
作用：创建一个数组
```

示例1：

```javaScript
let resArr = new Array()
console.log(resArr);// []
```

示例2:


```javaScript
let resArr = new Array(1, 2)
console.log(resArr);// [1, 2]
```


示例3:


```javaScript
let resArr = new Array([1, 2], 2)
console.log(resArr);//[[1, 2], 2]
```


### 3. copyWithin()
```	
语法： arr.copyWithin(target[, start[, end]])
返回值：改变后的arr
参数：
	1. target 复制的数组的某一部分到target下标的位置,如果target大于start，那么复制的序列会从start到end复制从target下标开始，超出数组长度的元素就不会复制成功，如示例1
	2. start 复制的起始下标，不设置代表复制从数组第一个元素开始
	3. end 复制的结束下标，不设置代表复制到数组结束
作用：复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度。
```


示例1：

```javaScript
let arr = [1, 2, 3, 4, 5]
let resArr = arr.copyWithin(4)
console.log(resArr);// [1, 2, 3, 4, 1]
```

示例2:


```javaScript
let arr = [1, 2, 3, 4, 5]
let resArr = arr.copyWithin(1, 2, 3)
console.log(resArr);// [1, 3, 3, 4, 5]
```


### 4. entries()
```	
语法：arr.entries()
返回值：新的Array Iterator对象
参数：
作用：
```

示例1：

```javaScript
let arr = ["hello", "hi", 4, 5]
let iteartor = arr.entries()
console.log(iteartor); //Array Iterator {}
console.log(iteartor.next().value) // [0, "hello"]
console.log(iteartor.next().value) // [1, "hi"]
console.log(iteartor.next().done) // true done表示迭代是否完成
```


### 5. every()
```	
语法： arr.every(callback[, thisArg])
返回值：布尔值
参数：
	1. callback函数 检测数组元素的函数
		callback接受三个参数element（检测数组当前的元素），index（检测数组当前的元素的下标），arr（被检测的数组）
	2. thisArg this指向
作用：检测arr数组的所有元素都能经过callback函数的检测，如果所有数组元素都通过才返回true，如果只有一个不通过都会返回false
```

示例1：

```javaScript
let arr = [1, 10, 4, 5];
function isBigTen (element, index, array) {
	console.log("element: "+ element + ";index: " + index + ";array: "+ array);
	/* element: 1;index: 0;array: 1, 10, 4, 5*/
	if (element > 10) {
		return true
	}
}
let res = arr.every(isBigTen,this)
console.log(res); // false
```

```javaScript
let res = [1, 10, 4, 5].every(x => x > 10);
console.log(res); // false
	
```



示例2:

```
let arr = [11, 110, 14, 15];
function isBigTen (element, index, array) {
	console.log("element: "+ element + ";index: " + index + ";array: "+ array);
	/* element: 11;index: 0;array: 11,110,14,15
element: 110;index: 1;array: 11,110,14,15
element: 14;index: 2;array: 11,110,14,15
 element: 15;index: 3;array: 11,110,14,15*/
	if (element > 10) {
		return true
	}
}
let res = arr.every(isBigTen,this)
console.log(res); // true
```

### 6. fill()
```	
语法： arr.fill(value[, start[, end]])
返回值：填充后的数组
参数：
	1. value 用来填充的数值
	2. start 填充的起始位置，不填，默认0
	3. end 填充的结束位置，不填，默认arr.length-1
作用：填充数组
```

示例1：

```javaScript
let arr = [1, 10, 4, 5];
arr = arr.fill("hello",0, 2)
console.log(arr); // ["hello", "hello", 4, 5]
```

### 7. filter()
```	
语法： var newArray = arr.filter(callback(element[, index[, array]])[, thisArg])
返回值：一个新数组
参数：和every一样
作用：找到数组中符合经过callback函数筛选出来的元素，返回到新数组里
```

```javaScript
function isBigTen(element) {
  return element >= 10;
}
var filtered = [12, 5, 8, 130, 44].filter(isBigTen);
console.log(filtered); // [12, 130, 44]
```


### 8. find()

```	
语法： arr.find(callback[, thisArg])
返回值：符合测试函数callback的第一个数组元素
参数：和every()一样
作用：找到第一个符合测试函数的数组元素
```

```javaScript
function isBigTen(element) {
  return element >= 10;
}
var filtered = [12, 5, 8, 130, 44].find(isBigTen);
console.log(filtered); // 12
```

### 9. findIndex()

```	
语法： arr.findIndex(callback[, thisArg])
返回值：符合测试函数callback的第一个数组元素下标
参数：和every()一样
作用：找到第一个符合测试函数的数组元素的下标
```


```javaScript
function isBigTen(element) {
  return element >= 10;
}
var filtered = [12, 5, 8, 130, 44].findIndex(isBigTen);
console.log(filtered); // 0
```

### 10. flat()

```	
语法： var newArray = arr.flat(depth)
返回值：一个新数组
参数：depth：遍历的深度
作用：将一个多维数组按照遍历的深度合成一个新的数组，例如把多维数组扁平化成1维数组
```

```javaScript
var flatRes = [12, 5, 8,[11, 130, "22", ["hello", 33]], 44].flat(3);
console.log(flatRes); //  [12, 5, 8, 11, 130, "22", "hello", 33, 44]
```
### 11. flatMap()

```	
语法： var new_array = arr.flatMap(function callback(currentValue[, index[, array]]) {
    // 返回新数组的元素
}[, thisArg])
返回值：一个新的数组，其中每个元素都是回调函数的结果，并且结构深度 depth 值为1。
参数：
	1. callback:可以生成一个新数组中的元素的函数，可以传入三个参数：
		* currentValue当前正在数组中处理的元素
		* index可选可选的。数组中正在处理的当前元素的索引。
		* array可选可选的。被调用的 map 数组
	2.	thisArg可选.执行 callback 函数时 使用的this值
作用：首先使用映射函数映射每个元素，然后将结果压缩成一个新数组
```

```javaScript
var flatMapRes = [12, 5, 8, "22", "hello", 33, 44].flatMap(x => [parseInt(x)*2]);
console.log(flatMapRes); //   [24, 10, 16, 44, NaN, 66, 88]
```

### 12. forEach()

```	
语法： arr.forEach(callback[, thisArg]);
返回值：undefined
参数：和flatMap一样
作用：forEach 方法按升序为数组中含有效值的每一项执行一次callback 函数，那些已删除或者未初始化的项将被跳过（例如在稀疏数组上
```

```javaScript
var arr = [];
var flatMapRes = [12, 5, 8, "22", "hello", 33, 44].forEach(x => arr.push(x));
console.log(flatMapRes); //  undefined
console.log(arr) // [12, 5, 8, "22", "hello", 33, 44]
```

### 13. includes()

```	
语法： arr.includes(valueToFind[, fromIndex])
返回值：true或false
参数：valueToFind： 被查找到元素。fromIndex：从下标fromIndex开始查找
作用：用来判断一个数组里是否包含某个元素，如果包含，则返回true，否则false
```


```javaScript
var res = [12, 5, 8, "22", "hello", 33, 44]. includes(33);
console.log(res); //  true
var res1 = [12, 5, 8, "22", "hello", 33, 44]. includes("hi");
console.log(res1); //  false
```


### 14. indexOf()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 15. join()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 16. keys()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 17. lastIndexOf()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 18. map()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 19. pop()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 20. push()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 21. reduce()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 22. reduceRight()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 23. reverse()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 24. shift()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 25. slice()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 26. some()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 27. sort()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 28. splice()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 29. toLocaleString()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 30. toString()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 31. unshift()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 32. values()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 33. from()
```	
语法： 
返回值：
参数：
作用：
示例：
```
### 34. isArray()
```	
语法： 
返回值：
参数：
作用：
示例：
```

### 32.of()
```	
语法： 
返回值：
参数：
作用：
示例：
```


