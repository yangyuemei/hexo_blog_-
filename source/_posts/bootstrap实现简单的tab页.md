---
title: bootstrap实现简单的tab页
date: 2017-03-21 15:15:16
tags: bootstrap
category: bootstrap
keywords:  #文章关键词，多个关键词用英文逗号隔开
layout: douban
comments: true

---

###  1. 引入对应的css、js文件

   ```javascript
   <link rel="stylesheet" href="https://cdn.static.runoob.com/libs/bootstrap/3.3.7/css/bootstrap.min.css">
   	<script src="https://cdn.static.runoob.com/libs/jquery/2.1.1/jquery.min.js"></script>
   	<script src="https://cdn.static.runoob.com/libs/bootstrap/3.3.7/js/bootstrap.min.js"></script>
   ```

### 2. 写一个ul,包含tab页标题

   ```javascript
   <ul id="myTab" class="nav nav-tabs">
   	<li class="active"><a href="#home" data-toggle="tab">菜鸟教程</a></li>
   	<li><a href="#ios" data-toggle="tab">iOS</a></li>
   	<li class="dropdown">
   		<a href="#" id="myTabDrop1" class="dropdown-toggle" data-toggle="dropdown">Java <b class="caret"></b></a>
   		<ul class="dropdown-menu" role="menu" aria-labelledby="myTabDrop1">
   			<li><a href="#jmeter" tabindex="-1" data-toggle="tab">jmeter</a></li>
   			<li><a href="#ejb" tabindex="-1" data-toggle="tab">ejb</a></li>
   		</ul>
   	</li>
   </ul>
   ```

### 3. 每一个tab对应的内容页

   ```javascript
   <div id="myTabContent" class="tab-content">
   	<div class="tab-pane fade in active" id="home">
   		<p>home</p>
   	</div>
   	<div class="tab-pane fade" id="ios">
   		<p>ios</p>
   	</div>
   	<div class="tab-pane fade" id="jmeter">
   		<p>jmeter</p>
   	</div>
   	<div class="tab-pane fade" id="ejb">
   		<p>ejb</p>
   	</div>
   </div>
   ```

###  4. tab页点击之后的状态

   ```javascript
   <script>
   $(function(){
   	$('a[data-toggle="tab"]').on('shown.bs.tab', function (e) {
   		// 获取已激活的标签页的名称
   		var activeTab = $(e.target).text();
   		// 获取前一个激活的标签页的名称
   		var previousTab = $(e.relatedTarget).text();
   		$(".active-tab span").html(activeTab);
   		$(".previous-tab span").html(previousTab);
   	});
   });
   </script>
   ```

   ​