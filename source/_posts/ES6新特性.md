---
title: ES:10大新特性
date: 2018-02-18 12:15:40
tags: ES6
category: ES6
---

# 1.ES6中的默认参数

### 传统用法定义默认参数
#### <font color="#0000ff">缺点：这样做一直都没什么问题，直到参数的值为0，因为0在JavaScript中算是false值，它会直接变成后面硬编码的值而不是0本身<font>
```javascript
var link = function (height, color, url) {
    var height = height || 50
    var color = color || 'red'
    var url = url || 'http://azat.co'
    ...
}
```
### ES6用法
```javascript
var link = function(height = 50, color = 'red', url = 'http://azat.co') {
  ...
}
```
# 2. ES6中的模版表达式
### ES5用法
模版表达式在其他语言中一般是为了在模版字符串中输出变量，所以在ES5中，我们非得把字符串破开变成这样：
```javascript
var name = 'Your name is ' + first + ' ' + last + '.'
var url = 'http://localhost:3000/api/messages/' + id
```
### ES6用法
在ES6中我们有了新语法，在反引号包裹的字符串中，使用${NAME}语法来表示模板字符:
```javascript
var name = `Your name is ${first} ${last}`
var url = `http://localhost:3000/api/messages/${id}`
```

# 3. ES6中的多行字符串
### 传统的写法
```javascript
var roadPoem = 'Then took the other, as just as fair,nt'
    + 'And having perhaps the better claimnt'
    + 'Because it was grassy and wanted wear,nt'
    + 'Though as for that the passing therent'
    + 'Had worn them really about the same,nt'
 
var fourAgreements = 'You have the right to be you.n
    You can only be you when you do your best.'
```
### 在ES6中，只要充分利用反引号
```javascript
var roadPoem = `Then took the other, as just as fair,
    And having perhaps the better claim
    Because it was grassy and wanted wear,
    Though as for that the passing there
    Had worn them really about the same,`
 
var fourAgreements = `You have the right to be you.
    You can only be you when you do your best.`
```
# 4. ES6中的拆包表达式
假如说你有一个简单的赋值表达式，把对象中的house的mouse赋值为house和mouse的变量。
```javascript
var data = $('body').data(), // 假设data中有mouse和house的值
  house = data.house,
  mouse = data.mouse
```
```javascript
var jsonMiddleware = require('body-parser').json
var body = req.body, // body中有用户名和密码值
  username = body.username,
  password = body.password
```
在ES6中我们可以用以下语句替换：
```javascript
var { house, mouse} = $('body').data() // 我们会拿到house和mouse的值的
 
var {jsonMiddleware} = require('body-parser')
 
var {username, password} = req.body
```
在数组中
```javascript
var [col1, col2]  = $('.column'),
  [line1, line2, line3, , line5] = file.split('n')
```
#5. ES6中改进的对象表达式
你能用对象表达式所做的是超乎想象的！类定义的方法从ES5中一个美化版的JSON，进化到ES6中更像类的构造。

这是一个ES5中典型的对象表达式，定义了一些方法和属性。

```JavaScript

var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]}

var accountServiceES5 = {
  port: serviceBase.port,
  url: serviceBase.url,
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf())
  },
  getUrl: function() {return 'http://' + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
```

```JavaScript
var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]}
 
var accountServiceES5 = {
  port: serviceBase.port,
  url: serviceBase.url,
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf())
  },
  getUrl: function() {return 'http://' + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
```

如果你想做的好看一点，我们可以用Object.create方法来让 serviceBase 成为 accountServiceES5 的 prototype 从而实现继承。


```JavaScript

var accountServiceES5ObjectCreate = Object.create(serviceBase)
var accountServiceES5ObjectCreate = {
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf())
  },
  getUrl: function() {return 'http://' + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
```

```JavaScript
var accountServiceES5ObjectCreate = Object.create(serviceBase)
var accountServiceES5ObjectCreate = {
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf())
  },
  getUrl: function() {return 'http://' + this.url + ':' + this.port},
  valueOf_1_2_3: getAccounts()
}
```
我知道 accountServiceES5ObjectCreate 和 accountServiceES5 是不完全相同的。因为一个对象 accountServiceES5 会有如下所示的 __proto__ 属性：


但对于这个示例，我们就把这两者考虑为相同的。所以在ES6的对象表达式中，我们把getAccounts: getAccounts简化为getAccounts,，并且我们还可以用__proto__直接设置prototype，这样听起来合理的多。（不过并不是用proto）


```JavaScript

var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]}
var accountService = {
    __proto__: serviceBase,
    getAccounts,
```

```JavaScript
var serviceBase = {port: 3000, url: 'azat.co'},
    getAccounts = function(){return [1,2,3]}
var accountService = {
    __proto__: serviceBase,
    getAccounts,
还有，我们可以调用 super 和动态索引(valueOf_1_2_3)
```
```JavaScript

// 续上段代码
    toString() {
     return JSON.stringify((super.valueOf()))
    },
    getUrl() {return 'http://' + this.url + ':' + this.port},
    [ 'valueOf_' + getAccounts().join('_') ]: getAccounts()
};
console.log(accountService)
```

```JavaScript
// 续上段代码
    toString() {
     return JSON.stringify((super.valueOf()))
    },
    getUrl() {return 'http://' + this.url + ':' + this.port},
    [ 'valueOf_' + getAccounts().join('_') ]: getAccounts()
};
console.log(accountService)
```