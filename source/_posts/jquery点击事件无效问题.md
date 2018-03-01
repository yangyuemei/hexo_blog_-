---
title: jquery点击事件无效问题
date: 2017-03-17 16:46:45
tags: jquery
category:  jquery
---

* ### 问题:ajax异步请求数据后,动态想table中追加行，行点击事件无效

* ### 原因:动态加入到dom中的对象无法继承原有的事件，故无效

* ### 解决办法
    #### 1. js方法：将td的点击事件写成函数

           ```javascript
           $("#table").append(<tr><td onclick=""></td></tr>);
           ```

    #### 2. jquery方法：利用事件委派机制(适用于jquery1.9版本以下)

           ```javascript
           $("#table").find("td").live('click',function(){});
           ```

    #### 3. jquery方法：适用于jquery1.7版本以上

           ```javascript
           $("#table").find("td").on('click',function(){});
           ```
