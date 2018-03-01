---
title: PHP实现简单分页过程
date: 2017-03-18 11:07:52
tags: php
category: php

---

### 1. 连接数据库

   ``` java
   $link=mysql_connect("localhost","root","root");//root为用户数据库用户名、密码
   mysql_select_db("db_name",$link);//db_name为数据库名
   mysql_query("set names gb2312");//设置字集
   ```

### 2. 得到5个值

   ```java
   $perNumber=2; //每页显示的记录数

   $page=$_GET['page']; //获得当前的页面值

   $count=mysql_query("select count(*) from tb_article"); 
   $result=mysql_fetch_array($count);
   $totalNumber=$result[0];//获得记录总数

   $totalPage=ceil($totalNumber/$perNumber); //计算出总页数

   $startCount=($page-1)*$perNumber;//计算偏移量
   ```

### 3. 判断当前页数

   ```java
   //如果没有值,则赋值1
   if (!isset($page)) {
     $page=1;
   } 
   ```

### 4. 根据上面的数值计算出开始的记录和记录数(即sql查询语句)

   ```java
   $rs=mysql_query("select * from tb_article limit $startCount,$perNumber");
   ```

### 5. while 循环输出每页记录数

   ```java
     while($row = mysql_fetch_array($rs)){
       <table><tr><td><?php echo $row[''];?></td></tr></table>
     }
   ```

### 6. 分页条的显示

    ​```java
   <?php
     if ($page != 1) { //页数不等于1
   ?>
    <ul class="pagination">
       <!--显示上一页-->
       <li><a href="main.php?page=<?php echo $page - 1;?>">上一页</a></li>
     </ul>
     <?php
      }
       for ($i=1;$i<=$totalPage;$i++) {  //循环显示出页面
     ?>
        <ul class="pagination">
          <li><a href="main.php?page=<?php echo $i;?>"><?php echo $i;?></a></li>
          </ul>
       <?php
        }
       if ($page<$totalPage) { //如果page小于总页数,显示下一页链接
         ?>
           <ul class="pagination">
            <li><a href="main.php?page=<?php echo $page + 1;?>">下一页</a></li>
          </ul>
         <?php
          }
     ?>
    ​```

### 7. 到此完成简单的分页