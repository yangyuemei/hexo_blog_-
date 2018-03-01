---
title: 基于webpack+node的vue项目搭建
date: 2017-03-18 10:09:20
tags: Vue
category: Vue
---
### 1.安装nodejs环境
> 1)去官网下载nodejs最新版本并安装
  2)测试是否安装成功  
```node
node -v
npm -v
```
### 2.初始化项目
> 1)新建一个文件夹 webpack-vue-demo
  2)进入webpack-vue-demo根目录 npm init

### 3.安装依赖包
> 1)npm i webpack vue vue-loader
  2)npm i webpack css-loader vue-template-compiler
  3)npm i webpack-dev-server style-loader url-loader
  4)npm i cross-env html-webpack-plugin

### 4.在webpack-vue-demo目录下新建src文件夹
> 1)在src文件夹下新建app.vue
  2)在src文件夹下新建index.js  

### 5.app.vue的代码如下
```js
<template>
  <div id="test">{{text}}</div>
</template>

<script>
export default {
  data(){
      return{
          text:'888'
      }
  }
}
</script>

<style>
#test{
    color:red;
}
</style>
```
### 6.index.js的代码如下
```js
import Vue from 'vue'
import App from './app.vue';

const root=document.createElement('div')
document.body.appendChild(root)

new Vue({
    render: (h) => h(App)
}).$mount(root)
```
### 7.webpack-vue-demo根目录下新建webpack.config.js,代码如下
```js
const path = require('path')
const webpack = require('webpack')
const HTMLPlugin = require('html-webpack-plugin')

const isDev = process.env.NODE_ENV === 'development'

const config = {
    target:'web',//浏览器
    entry:path.join(__dirname,'src/index.js'),
    output:{
        filename:'bundle.js',
        path:path.join(__dirname,'dist')
    },
    module: {
        rules:[
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            },
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            }
        ]
    },
    plugins:[
        new webpack.DefinePlugin({
            'process.env':{
                NODE_ENV: isDev ? '"development"' : '"production"'
            }
        }),
        new HTMLPlugin() //html模板
    ]
}
if(isDev){
    config.devtool = '#cheap-module-eval-source-map'//代码调试
    config.devServer = {
       port: 8002,
       host: '0.0.0.0',
       overlay:{
           errors:true
       },
       hot:true,//不需要重新刷新整个页面
       open:true //自动打开浏览器 
    }
    //热加载
    config.plugins.push(
        new webpack.HotModuleReplacementPlugin(),
        new webpack.NoEmitOnErrorsPlugin()
    )
}
module.exports = config
```
### 8.在package.json下加入以下代码
```js
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "cross-env NODE_ENV=production webpack --config webpack.config.js",
    "dev": "cross-env NODE_ENV=development webpack-dev-server --config webpack.config.js"
  },
```
### 9.打包
```js
npm run build
```
### 10.运行
```js
npm run dev
```

### 11.从github上down下来并运行
> 1)git clone https://github.com/yymuy/webpack-vue-demo.git
  2)npm install
  3)npm run dev