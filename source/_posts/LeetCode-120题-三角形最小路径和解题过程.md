---
title: LeetCode 120题 三角形最小路径和解题过程
date: 2020-07-30 22:39:17
tags: 算法
categories: 算法
---

## 前言

最近一两个月每天下班去健身房锻炼1到2个小时，回到家比较晚，又累（借口），所以就没有刷力扣了。

最近感觉，不行了，还是要继续刷题，不能太颓废。所以又开始刷题之旅。

之前一想到动态规划，什么状态方程，状态转移，看到就很头疼，现在开始攻克他。

这道题我还没有出生的时候就已经出现，是比我还老的一道经典题，用它来理解动态规划是比较好的。

## 题目

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

相邻的结点 在这里指的是 下标 与 上一层结点下标 相同或者等于 上一层结点下标 + 1 的两个结点。

 

例如，给定三角形：

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]	
]
```	

自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。

说明：

如果你可以只使用 O(n) 的额外空间（n 为三角形的总行数）来解决这个问题，那么你的算法会很加分。

## 解题思路及代码


其实我们可以把这个想象成一道数学题。

写数学题第一步是什么，写假设，假设x是什么，y是什么，然后找出x,y之间的关系。

这道题也是这样的。

### 动态规划

首先我们要知道它是要找到自顶向下的最小路径和，所以我们需要用一个数组去存储从顶到每个坐标的最小路径和，这样，我们算到最后一行的时候，只需要到比较最后一行到时候到最小值。

所以dp[i][j]代表着从顶到该坐标（i，j）的最小路径和，假设行数是row，列数是col，所以我们最后只需要找到第row行中最小的dp[row - 1 ][j]（0 <= j < col）

然后移动的时候是有条件的，每一步只能移动到下一行中相邻的结点上。

所以我们可以得到常规情况下:

```
dp[i][j] = Math.min(dp[i - 1][j], dp[i - 1][ j - 1]) + triangle[i][j]
```

然后我们考虑边界情况，左边界的话，也就是j===0的时候：

```
dp[i][j] = dp[i - 1][j]+ triangle[i][j] 
```

右边界，也就是 i===j的时候

```
dp[i][j] = dp[i - 1][j - 1]+ triangle[i][j] 
```

所以我们很容易得到如下代码

```
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function(triangle) {
    let row = triangle.length
    if(row === 0) return 0
    let col = triangle[row - 1].length
    let dp = Array.from({length: row}, x => Array.from({length: col}))
    dp[0][0] = triangle[0][0]
    for (let i = 1; i < row; i++) {
        for (let j = 0; j <= i; j++) {
            if (j === 0) {
                dp[i][j] = dp[i - 1][j]+ triangle[i][j] 
            }else if (i === j) {
                dp[i][j] = dp[i - 1][j - 1]+ triangle[i][j] 
            }else {
                dp[i][j] = Math.min(dp[i - 1][j], dp[i - 1][ j - 1]) + triangle[i][j]
            }
        }
    }
    let min = Math.min(...dp[row - 1])
    return min
};
```

### 优化1 - 时间

首先我们知道最后返回的是一个最小路径和，我们从顶到下去计算的话，最后要去判断一下最后一行中的最短路径的最小值，那么我们反过来呢，逆向思维，我们从底部开始往上走，最后我们走到顶的时候只有一个值了，那个值就是我们要找的最小值,这样就不需要去判断边界条件了。

所以我们可以把遍历的稍稍改动一下：

```
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function(triangle) {
    let row = triangle.length
    if(row === 0) return 0
    let col = triangle[row - 1].length
    let dp = Array.from({length: row}, x => Array.from({length: col}).fill(0))
    for (let k = 0; k < col; k++) {
        dp[row - 1][k] = triangle[row - 1][k]
    }
    for (let i = row - 2; i >= 0; i--) {
        for (let j = 0; j <= i; j++) {
            dp[i][j] = Math.min(dp[i + 1][j], dp[i + 1][ j + 1]) + triangle[i][j]
        }
    }
    return dp[0][0]
};
```

### 优化2 - 空间

我们前面的方法都是用的二维数组存储每个坐标上的最小路径和，比如我们计算第二行的最小路径和的时候，第四行的数据我们已经用不上了，因为第三行的数据把第四行的数据加上了，所以其实我们只需要维护一个长度为col的数组，每次计算后将上次的值覆盖就可以了，

```
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function(triangle) {
  let row = triangle.length
  if (row === 0) return 0
  let dp = new Array(row +1).fill(0)
  for (let i = row - 1; i >=0; i--) {
    for (let j = 0; j <= i; j++) {
      dp[j] = Math.min(dp[j], dp[j+1]) + triangle[i][j]
    }
  }
  return dp[0]
};
```