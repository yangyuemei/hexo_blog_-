---
title: for循坏之5大算法
date: 2017-03-16 18:50:10
tags: JavaScript
category: JavaScript
---



 ```javascript
 var sort={ 
  //初始化
   init:function(){
      var tempArr=[3,6,4,2,11,10,5];
      sort.bubbleSort(empArr);
      },
 ```
 ```javascript
   //打印到控制台
   debug:function(str){
      if(window.console && window.console.log){
           console.log(str);
       }
   },
 ```
 ```javascript
   //数组数据交换
   swap:function(arr,index1,index2){
     var temp = arr[index1];
     arr[index1] = arr[index2];
     arr[index2] = temp;
   },
 ```
 ```javascript
   //冒泡排序  
   bubbleSort:function(arr){ 
     // this.debug("冒泡排序前的数组为:"+arr);
     var len = arr.length;
     for(var i = 0;i<len-1;i++){//比较的轮数为数组的总个数-1
       for(var j = 0;j<len-i-1;j++){//每轮比较的次数
           if(arr[j]  arr[j+1] ){ //arr[j]  arr[j+1]为升序  arr[j] < arr[j+1]为降序
               this.swap(arr,j,j+1);
           }
       }
       this.debug("第"+(i+1)+"轮冒泡排序后:"+arr);
   }
   this.debug("冒泡排序后的数组为:"+arr);
   },
 ```
```javascript
  //选择排序
  selectionSort:function(arr){
    // this.debug("选择排序before:"+arr);
      var len = arr.length;
      var min;
      for (var i = 0; i < len -1; i++) {
          min = i;
          // 比较最小项目和第i项之后的剩余数组项, 以寻找更小项
          for (var j = i+1; j < len; j++) {
              if (arr[j] < arr[min]) { //arr[j] < arr[j+1]为升序  arr[j]  arr[j+1]为降序  
                  min = j;
                  this.debug("min--"+min);
              }
          }
          this.swap(arr,i, min);
          // this.debug("第"+(i+1)+"轮选择排序后:"+arr);
      }
      this.debug("选择排序after:"+arr);
  },
```
 ```javascript
   //快速排序
   quickSort:function(arr){ 
       // this.debug("快速排序before:"+arr);
       var quick = function(arr){
           var len = arr.length,
               left = [],
               right = [],
               pivot;
               //meCall的作用是指向拥有arguments对象的函数
               // meCall = arguments.callee;  //在函数内部，有两个特殊的对象：arguments 和 this。其中， arguments 的主要用途是保存函数参数， 但这个对象还有一个名叫 callee 的属性，该属性是一个指针，指向拥有这个 arguments 对象的函数。
           if(len < 1){
               return -1;
           }
           pivot = arr[0];//选取数组第一个为基准进行分区
           for(var i = 0;i < len-1; i++){
               if(arr[i] < pivot ){
                   left.push(arr[i]); //小于基准的放左边  放左边的那一堆又以第一个为基准 如此循环
               }
               else{
                   right.push(arr[i]);//大于基准的放右边  放右边的那一堆也以第一个为基准 如此循环
               }
           }
           return arr.concat(left,right);
           // return meCall(left).concat(pivot,meCall(right));
         //arrayObject.concat(arrayX,arrayX,......,arrayX) 方法用于连接两个或多个数组 arrayX参数是必需的
       }
       this.debug("快速排序after:"+arr);
       return quick(arr);
   },
 ```
```javascript
  //插入排序    
  insertionSort:function(arr){
     // this.debug("插入排序before:"+arr);
      var temp,inner,len = arr.length;
      for (var i = 0; i < len-1 ; i++) {
          temp = arr[i];
          inner = i;
          while(inner0 && arr[inner-1] = temp){
              arr[inner] = arr[inner-1];
              --inner;
          }
          arr[inner] = temp;
          // this.debug("第"+(i+1)+"轮插入排序后:"+arr);
      }
      this.debug("插入排序after:"+arr);
  },
```
```javascript
  //归并排序   
  mergeSort2:function(arr){ 
      this.debug("归并排序before:"+arr);
      var len = arr.length;
      if(len  1) {
        var index = Math.floor(len / 2);
        left = arr.slice(0,index); //得到下标从0~index-1的数组
        right = arr.slice(index);  //得到下标从index开始到末尾的数组
        return this.merge2(mergeSort2(left),mergeSort2(right));  
      }
      else {
        return arr;
      }
      this.debug("归并排序after:"+arr);
  },
  merge2:function(left,right){ //采用递归
      var arr = [];
          while(left.length && right.length) {
            if(left[0] < right[0]) {
              arr.push(left.shift());
          }
          else {
             arr.push(right.shift());
           }
         }
         return arr.concat(left,right);
  },
```
```javascript
  //二分插入排序
  binaryInsertSort:function(arr){
      // this.debug("二分插入排序before:"+arr);
      for (var i = 1; i < arr.length; i++) {
      var key = arr[i], 
          left = 0, 
          right = i - 1;
      while (left <= right) {
        // var middle = parseInt((left + right) / 2);
        var middle = Math.floor((left + right) / 2);
        if (key < arr[middle]) {
          right = middle - 1;
        } 
        else {
          left = middle + 1;
        }
      }
      for (var j = i - 1; j = left; j--) {
        arr[j + 1] = arr[j];
      }
      arr[left] = key;
      // this.debug("第"+(i+1)+"轮二分排序后:"+arr);
    }
     this.debug("二分插入排序after:"+arr);
  },
```
```javascript
  //希尔排序
  shellSort:function(arr){
      // this.debug("希尔排序before:"+arr);
      // var gaps = [5,3,1],  //增量分组  第一次5个数为一组  第二次3个数为一组  第三次1个数为一组
      //     temp;
      // for(var g = 0;g <gaps.length; g++){
      //     for(var i = gaps[g];i<arr.length;i++){
      //         temp = arr[i];
      //         for(var j = i;j = gaps[g] && arr[j-gaps[g]]  temp;j -= gaps[g]){
      //             arr[j] = arr[j-gaps[g]];
      //         }
      //         arr[j] = temp;
      //     }
      //     // this.debug("第"+(g+1)+"轮希尔排序后:"+gaps);
      // }
        var i,k,j,len=arr.length,gap = Math.ceil(len/2),temp;
        while(gap0){
          for (var k = 0; k < gap; k++) {
              var tagArr = [];
              tagArr.push(arr[k])
              for (i = k+gap; i < len; i=i+gap) {              
                  temp = arr[i];
                  tagArr.push(temp);
                  for (j=i-gap; j -1; j=j-gap) {
                      if(arr[j]temp){
                          arr[j+gap] = arr[j];
                      }else{
                          break;
                      }
                  }
                  arr[j+gap] = temp;
              }
              console.log(tagArr,"gap:"+gap);//输出当前进行插入排序的数组。
              // console.log(arr);//此轮排输出序后的数组。
          }
          gap = parseInt(gap/2);
      }
      this.debug("希尔排序after:"+arr);
      return arr;   
  },
```
```javascript
  //A* 排序  
  aAtarSort:function(){   
      Open = [起始节点]; Closed = [];  
      // while ( Open表非空 )  
      // {  
      // 从Open中取得一个节点X，并从OPEN表中删除。  
      // if (X是目标节点)  
      // {  
      // 求得路径PATH；返回路径PATH；  
      // }  
      // for (每一个X的子节点Y)  
      // {  
      // if( Y不在OPEN表和CLOSE表中 )  
      // {  
      // 求Y的估价值；并将Y插入OPEN表中；//还没有排序  
      // }  
      // else  
      // if( Y在OPEN表中 )  
      // {  
      // if( Y的估价值小于OPEN表的估价值 )  
      // 更新OPEN表中的估价值；  
      // }  
      // else //Y在CLOSE表中  
      // {  
      // if( Y的估价值小于CLOSE表的估价值 )  
      // {  
      // 更新CLOSE表中的估价值；  
      // 从CLOSE表中移出节点，并放入OPEN表中；  
      // }  
      // }  
      // 将X节点插入CLOSE表中；  
      // 按照估价值将OPEN表中的节点排序；  
      // }//end for  
      // }//end while  
  },
```
 ```javascript
   //线性查找
   linearSearch:function(arr,data){
      for(var i = 0;i<arr.length;i++){
           if(arr[i] == data){
               return i;
           }
       }
       return -1;
   },
 ```
 ```javascript
   //二分查找 适用于已排好序的线性结构
   binarySearch:function(arr,data){
       var lower = 0,
           high = arr.length - 1,
           mid;
       while(lower <= high){
           mid = Math.floor((lower+high)/2); //Math.floor() 求一个最接近它的整数,它的值小于或等于这个浮点数
           if(arr[mid] < data){
               lower = mid + 1;
           }else if(arr[mid]  data){
               high = mid - 1;
           }else{
               return mid;
           }
           return -1;
       }
   },
}
 ```
**使用：**

```javascript
var tempArr = [3,6,4,2,11,10,5];
sort.bubbleSort(tempArr); //冒泡
```