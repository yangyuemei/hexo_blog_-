---
title: ES6的坑
date: 2018-02-18 12:15:40
tags: ES6
category: ES6
---

# ES6的Promise
### 问题1
```javascript
const promise = new Promise((resolve, reject) => {
  console.log(1)
  resolve()
  console.log(2)
})
promise.then(() => {
  console.log(3)
})
console.log(4)
```
### 运行结果
```javascript
1
2
4
3
```
### <font color="#0000ff">解释：Promise 构造函数是<font color="red">同步</font>执行的，promise.then 中的函数是<font color="red">异步</font>执行的。</font>