---
title: 关于JavaScript数组你必须知道的几点
categories: [other]
---
# 关于JavaScript数组你必须知道的几点

## splice和slice区别

    arr.splice(start,deleteCount,insertItem,insertItem,....); 会改变原始数组,返回删除的数组
    arr.slice(start,end);浅拷贝start到end(不包含end）原始数组项
    
## 数组实现队列
    let a = [1, 2, 3];
    a.length; // 3
    a.pop(); // 3
    console.log(a); // [1, 2]
    a.length; // 2
    
    pop移除 arr.length-1位置的数组项 pop移除 arr.length-1位置的数组项
    
    let a = [1, 2, 3];
    let b = a.shift();
    console.log(a); 
    // [2, 3]
    console.log(b); 
    // 1
    
    shift移除 0位置的数组项
    
    所以 push和pop可以实现栈,push和 shift可以实现队列
    
    
    
    
    
    

## 其他
* [Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)



