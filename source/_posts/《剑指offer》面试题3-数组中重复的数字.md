---
title: 《剑指offer》面试题3 数组中重复的数字
date: 2020-12-03 21:42:48
tags: 算法
categories:
---

# 《剑指offer》面试题3 数组中重复的数字

## 题目描述


找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3

限制：
2 <= n <= 100000

```

来源：力扣（LeetCode）


## 题目解析

### 方法一  双层循环对比

a:  [2, 3, 1, 0, 2, 5, 3]

b:  [2, 3, 1, 0, 2, 5, 3]

拿第一层循环数组的i依次对比第二层循环的数组的i+1元素。

a 取2，然后分别遍历[3,1,0,2,5,3], 如果有重复的，就return，没有的话就i+1，依次类推。

代码如下

```
var findRepeatNumber = function(nums) {
  	let len = nums.length;
 	 for (let i = 0; i < len; i++) {
  		for (let j = i+1; j < len; j++) {
  			if (nums[i] === nums[j]){
  				return nums[i]
  			}
  	 	 }
	 }
};
```

因为有两层遍历，所以时间复杂度是O(n^2)

### 方法二 一层循环 + 哈希表

1. 首先定义一个Map
2. 然后遍历数组，判断Map里没有这个值，没有的话set一下，有的话说明这个值已经重复了，所以可以直接输出

代码如下

```
var findRepeatNumber = function(nums) {
    let map = new Map()
    let len = nums.length
    for (let i =0; i<len;i++) {
        if (map.has(nums[i])){
            return nums[i];
        } else {
            map.set(nums[i], 1)
        }
    }
};
```

因为只有一层遍历，所以时间复杂度是O(n)

## 总结

从时间复杂度上看，当然是建议使用方法二。

