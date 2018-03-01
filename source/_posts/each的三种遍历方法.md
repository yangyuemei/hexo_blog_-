---
title: each的三种遍历方法
date: 2017-03-17 16:35:50
tags: jquery
category: jquery
---

###  1.  选择器+遍历

``` javascript
$('div').each(function (i){
   i就是索引值
   this 表示获取遍历每一个dom对象
});
```

###  2.  选择器+遍历

``` javascript
$('div').each(function (index,domEle){
   index就是索引值
  domEle 表示获取遍历每一个dom对象

});
```

###  3.  常用的遍历方法

``` javascript
$.each(d,function (index,domEle){
  d是要遍历的集合
  index就是索引值
  domEle 表示获取遍历每一个dom对
});
```