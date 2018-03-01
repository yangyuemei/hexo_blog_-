---
title: ES6学习笔记
date: 2018-02-18 12:15:40
tags: ES6
category: ES6
---

# 1.let和const
### es6新增了let命令
### ①let局部变量  var局部变量
### ②let不存在变量提升  var存在变量提升
### ③暂时性死区 只要块级作用域存在let，它所声明的变量就在绑定在这个区域，不受外部影响
### ④let在相同的作用域内(模块内部)，不允许重复声明，模块与模块之间可以
### let为块级作用域，在块级{}之外访问不到
### 为什么需要块级作用域
> ES5只有全局作用域和函数作用域，没有块级作用域
内层变量可能会覆盖外层变量
用来计数的循环变量泄露为全局变量  
### let实际上是为javascript新增了块级作用域 
### 立即执行函数 (function(){}())
```javascript
var b = 200;
{
    console.log(b) /* undefined */
    var a = 12;
    let b = 10;
    console.log(b) /* 10 */
}
console.log(a) /* 12 */
console.log(b) /* undefined */
```
### const为不可变常量(物理内存地址不可变)
### const一旦声明，常量的值就不能改变
### const块级作用域 
### const暂时性死区 
### const不可重复声明 
```javascript
{
    const a = 10;
    console.log(a) /* 10 */
    a = 15; /* 此时报错 a is read-only */
    var a = 1000;
}
console.log(a) /*此时报错*/
```
### const对象
```javascript
const a = {
    name:"A"
}
a.name="B";/* 此时正确 */
```
### const数组
```javascript
const arr = [];
arr.push("Hello"); /* 此时正确 */
arr = ["Hello"]; /* 错误用法 */
```
### const对象冻结
```javascript
const person = Object.freeze({
    name:"zhangsan",
    age:12
});
consle.log(person.name)
consle.log(person.age)
consle.log(person)
```
### 彻底冻结对象的函数
var constantize = (obj) => {
    Object.freeze(obj);
    Object.keys(obj).forEach((key,value) => {
        if(typeof obj[key] === 'object'){
            constantize(obj[key])
        }
    })
}

# 2.跨模块常量
```javascript
/* module.js */
export const intVariantName = 100;
export const FloatVariantName = 3.1415677;
export const CharVariantName = "variantvariantalue";

/* use.js */
import * as variant from 'module.js' 
import {intVariantName,FloatVariantName} as variant from 'module.js' 
import intVariantName as variant from 'module.js'

console.log(variant.intVariantName)
console.log(variant.FloatVariantName)
console.log(variant.CharVariantName)  
```
# 3.全局变量属性
### var声明的全局变量属于全局对象的属性
```js
var varName = "varValue";
//浏览器环境下
console.log(window.varName)
//Node.js环境下
console.log(global.varName)
//通用环境
console.log(this.varName)
```
### let声明的全局变量不属于全局对象的属性
```js
var letName = "letValue";
//浏览器环境下
console.log(window.letName) //undefined
//通用环境
console.log(this.letName) //undefined
```
# 4.数组的解构赋值
### ES5写法
```js
var a = 1;
var b = 2;
var c = 3;
console.log(a)
console.log(b)
console.log(c)
```
### ES6写法 =的左边和右边结构相等
```js
var [a,b,c] = [1,2,3]
console.log(a)
console.log(b)
console.log(c)
```
```js
let [one,[[two],three]] = [1,[[2],3]
console.log(a)
console.log(b)
console.log(c)
```
```js
let [one, ,three]] = [1,2,3]
console.log(a)
console.log(c)
```
```js
let [head, ...tail] = [0,1,2,3]
console.log(head) //0
console.log(tail) //1,2,3
```
### 数组解构不成功 它的值都默认是undefined
```js
var [temp] = [];
console.log(temp) //undefined
var [first,second] = [100];
console.log(first) //100
console.log(second) //undefined
```

# 5.不完全解构 多给值少变量
=左边的模式，只匹配一部分右边的数组
严格匹配
```js
let [x,y] = [1,2,3]
console.log(x) //1
console.log(y) //2
```
```js
let [a,[b],c] = [1,[2,3],4]
console.log(a) //1
console.log(b) //2
console.log(c) //4
```
# 6.指定默认值
### 一个变量的情况
```js
var [temp = "string"] = [];
console.log(temp) //string

var [temp = "string"] = ["tempString"];
console.log(temp) //tempString
```

### 多个变量的情况
```js
var [x = "aaa",y] = ["bbb"]
console.log(x) //bbb
console.log(y) //undefined  

var [m,n = "bbb"] = ["ccc"]
console.log(m) //ccc
console.log(n) //bbb  

var [p,q = "bbb"] = ["ccc",undefined]
console.log(p) //ccc
console.log(q) //bbb
```

### 非遍历解构 --报错
```js
var [temp] = 1; //--error
var [temp] = false; //--error
var [temp] = NaN; //--error
var [temp] = undefined; //--error
var [temp] = null; //--error
```
### Iterator
```js
let [a,b,c] = new Set(["a","b","c"])
console.log(a) //a
console.log(b) //b
console.log(c) //c
```
# 7.对象的解构赋值
### 对象没有次序,key要一致
```js
let {name,age,id} = {id:"007",name:"zhangsan",age:22}
console.log(name) //zhangsan
console.log(age)  //22
console.log(id)   //007
```
### 变量名与属性名不一致
```js
let {person_name,person_age,person_id} = {id:"007",name:"zhangsan",age:22}
console.log(person_name) //undefined
console.log(person_age)  //undefined
console.log(person_id)   //undefined  

let {name:person_name,age:person_age,id:person_id} = {id:"007",name:"zhangsan",age:22}
console.log(person_name) //zhangsan
console.log(person_age)  //22
console.log(person_id)   //007 
```
```js
let {x = 3} = { x:undefined }
console.log(x)   //3 

let {y = 3} = { x:null }
console.log(y)   //null 
```

### 已声明变量的解构赋值
```js
var x;
({x} = {x:1})
```
# 8.字符串的解构赋值
### 字符串转换成了类似数组的对象
```js
cobst [a,b,c,d,e] = "Hello";
console.log(a)   //H 
console.log(b)   //e 
console.log(c)   //l 
console.log(d)   //l 
console.log(e)   //o 
```
###字符串的属性解构
```js
let { length:len } = "Hello"
```
# 9.函数参数的解构赋值
```js
function sum(x,y){
    return x+y;
}
console.log(sum(1,2))   //3
```
### 函数参数的解构赋值也可以使用默认值
```js
function sum({x=0,y=0} = {}){
    return [x,y];
}
console.log(sum({x:1,y:2}))   //[1,2]
console.log(sum({x:1}))       //[1,0]
console.log(sum({}))          //[0,0]
console.log(sum())            //[0,0]
```
```js
function sum({x,y} = {x:0,y:0}){
    return [x,y];
}
console.log(sum({x:1,y:2}))   //[1,2]
console.log(sum({x:1}))       //[1,undefined]
console.log(sum({}))          //[undefined,undefined]
console.log(sum())            //[undefined,undefined]
```
# 10.解构赋值的用途
### 1)交换变量的值
```js
//ES5
var a = 100;
var b = 200;

var temp;
temp = a;
a = b;
b = temp;

console.log(a) //200
console.log(b) //100
```
```js
//ES6
var a = 100;
var b = 200;

[x,y] = [y,x]

console.log(x) //200
console.log(y) //100
```
### 2)从函数返回多个值
```js
//返回一个数组 只取其中数组的其中一个
function fun(){
    return [1,2,3]
}
let [x,y,z] = fun();
console.log(x) //1
console.log(y) //2
console.log(z) //3
```
```js
//返回一个对象 只取其中对象的其中一个key
function fun(){
    return {
        id  :"007",
        name:"zhangsan",
        age :22
    }
}
let {x,y,z} = fun();
console.log(x) //007
console.log(y) //zhangsan
console.log(z) //22
```
### 3)函数参数的定义
```js
//参数是一组有次序的值 数组[]
function fun([x,y,z]){
    //x = 100;
    //y = 200;
    //z = 300;
}
fun([100,200,300])
```
```js
//参数是一组无次序的值 对象{}
function fun({x,y,z}){
    //x = 100;
    //y = 300;
    //z = 200;
}
fun({x:100,z:200,y:300})
```
### 4)提取json数据
```js
//
let jsonData = {
    id:"007",
    name:"zhangsan",
    age:22,
    score:{
        A:98,
        B:148,
        C:138
        }
}
console.log(jsonData)

//ES5
console.log("id----"+jsonData.id)
console.log("name----"+jsonData.name)
console.log("age----"+jsonData.age)
console.log("score0----"+jsonData.score[0])
console.log("score1----"+jsonData.score[1])
console.log("score2----"+jsonData.score[2])

//ES6
let {id,name,age,score:score} = jsonData;
console.log("id----"+id)
console.log("name----"+name)
console.log("age----"+age)
console.log("A----"+score.A)
console.log("B----"+score.B)
console.log("C----"+score.C)
```
### 5)函数参数的默认值
### 6)遍历Map结构
```js
let map new Map();
map.set("id","007");
map.set("name","zhangsan");
map.set("age",22);

//获取键 值
for(let [key,value] of map){
    console.log(key + "is" + value)
}

//获取键
for(let [key] of map){
    console.log(key)
}

//获取值
for(let [,value] of map){
    console.log(value)
}
```
### 7)输入模块的指定方法
```js
export const a;
import * as a from '';
```
 

