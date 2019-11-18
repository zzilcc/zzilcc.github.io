---
title: JS实现常用排序算法
date: 2019-08-04 14:34:15
tags: 排序算法
categories: 算法
---

## 前言

我们生活中排序无处不在，比如考试结束后，老师需要对学生成绩由高到低进行排序，还有我们排名单时有时候也按照字典序排序等等，下面就介绍几种常用的排序算法及js实现。

<!--more-->

## 冒泡排序

冒泡排序，顾名思义，就是一个个向上冒泡。具体思想是比较两个相邻的项，如果第一个比第二个大，那么就交换它们。用两层for循环去实现，所以第一次循环后，最大的那个数到达了最右边，下一次循环第二大的数就紧挨着最大的数，以此类推。

```js
function change (arr, index1, index2){
	let temp = arr[index1];
	arr[index1] = arr[index2];
	arr[index2] =temp;
}
```


```js
function bubbleSort (arr) {
	let len = arr.length;
	for (let i = 0; i < len; i++) {
		for(let j = 0; j < len; j++) {
			if (arr[j] > arr[j+1]) {
				change(arr, j, j+1);
			}
		}
	}
	return arr
}
```

我们可以看到冒泡排序的时间复杂度是O(n^2)。所以冒泡排序运行时间相对来说是比较久的。

比如数组是[2,4,1,6,9,7,5],第一轮循环后数组为[2,1,4,6,7,5,9],第二轮循环后数组为[1,2,4,6,5,7,9],我们知道第一轮循环后，最后一个数肯定是最大的。所以第二轮最后不应该去比较7和9。第三轮也是如此，不应该比较6，7，9。

所以我们可以改进一下冒泡排序，我们内循环的次数减去外循环中已跑过的轮数。

```js
function bubbleSort (arr) {
	let len = arr.length;
	for (let i = 0; i < len; i++) {
		for(let j = 0; j < len-1-i; j++) {
			if (arr[j] > arr[j+1]) {
				change(arr, j, j+1);
			}
		}
	}
	return arr
}
```



## 选择排序



## 插入排序

## 归并排序

## 快速排序

## 堆排序

