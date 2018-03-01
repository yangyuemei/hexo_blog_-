---
title: less学习笔记
date: 2018-02-17 16:46:45
tags: less
category:  less
---

# 1.什么是LESSCSS
ESSCSS是一种动态样式语言，属于CSS预处理语言的一种
# 2.变量  
## less源码：
<font color="#0000ff">定义变量：@color:red;</font>
<font color="#0000ff">使用变量：color:@color;</font>
```css
@color:red;
.header{
    color:@color
}
```
## 编译后的CSS：  

```css
.header{
    color:red
}
```
# 3.注释  

<font color="#0000ff">//    在less可见,css不可见</font>
<font color="#0000ff">/**/     在less、css可见</font>
# 4.混合（Mixins）
混合可以将一个定义好的class A轻松的引入到另一个class B中，从而简单实现class B继承class A中的所有属性。我们还可以带参数地调用，就像使用函数一样。

## less源码：
```css
.borderRadiu(@radius: 5px){
    border-radius:@radius
}
.header1{
    .borderRadiu()
}
.header2{
    .borderRadiu(10px)
}
```
## 编译后的CSS：
```css
.header1{
    border-radius:5px
}
.header2{
    border-radius:5px
}
```
# 5.嵌套
我们可以在一个选择器中嵌套另一个选择器来实现继承，这样很大程度减少了代码量，并且代码看起来更加的清晰。
## less源码：
```css
.header{
    p{
        color:red;
        a{
            text-align:center;
            &:hover{
                color:green
            }
        }
    }
}
```
## 编译后的CSS：
```css
.header p{
    color:red;
}
.header p a{
    text-align:center;
}
.header p a:hover{
    color:green
}
```
# 5.运算
优先值运算使用()区分  
颜色值运算：颜色值black->rgb模式#000000->16进制  
rgb模式范围：0~255，超出255将以255计算  

## less源码：
```css
.header{
    width:(400-100)*2px;
    color:#ffffff-55;
}
```
## 编译后的CSS：
```css
.header{
    width:600px;
    color:#c8c8c8;
}
```

# 6.命名空间
参考容器内元素的样式属性进行封装，并灵活调用
## less源码：
```css
.div1{
    text-align:center;
    .btn1{
        color:#fff;
        &:hover{
            color:#666;
        }
        .btn2{
            solor:red;
        }
    }
}
.div2{
    .div1 > .btn1;
}
```
## 编译后的CSS：
```css
.div2 .btn1{
    color:#fff;
}
.div2 .btn1:hover{
    color:#666;
}
.div2 .btn2{
    color:red;
}
```

# 7.作用域
首先会从本地查找变量或者混合模块，如果没找到的话会去父级作用域中查找，直到找到为止。
<font color="#0000ff">当前作用域  父级作用域  全局作用域  离他最近的</font> 
## less源码：
```css
@color:red; /*3.全局作用域*/
.bgcolor{
    p{
        @color:green; /*1.当前作用域*/
        color:@color;
    }
    @color:blue; /*2.父级作用域*/
}
@color:white; /*4.离他最近的作用域*/
```
## 编译后的CSS：
```css
bgcolor p{
    color:green; /*1.当前作用域*/
}
bgcolor p{
    color:blue; /*2.父级作用域*/
}
bgcolor p{
    color:red; /*3.全局作用域*/
}
bgcolor p{
    color:white;/*4.离他最近的作用域*/
}
```

# 8.引入 import 
### 1.引入文件 @import "style" "style.less"
### 2.使用变量 color:@color

# 9.关键字 !important 
# 10.条件表达式
# 11.循环 
# 9.关键字 !important 




