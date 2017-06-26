---
title: JavaScript 数据类型转化
categories: [JavaScript]
---
# Hexo 使用总结

## parseInt、parseFloat、Number区别
    var valStr="111a";
    console.log("parseInt="+parseInt(valStr));
    //111
    console.log("parseFloat="+parseFloat(valStr));
    //111
    console.log("Number="+Number(valStr));
    //NaN
     console.log("Number="+Number("''"));
    //NaN
    Number("11.22")
    //11.22
## 自动转换
**自动转化是以强制转化为基础**  

    // 1. 不同类型的数据互相运算
    123 + 'abc' // "123abc"
    
    // 2. 对非布尔值类型的数据求布尔值
    if ('abc') {
      console.log('hello')
    }  // "hello"
    
    // 3. 对非数值类型的数据使用一元运算符（即“+”和“-”）
    + {foo: 'bar'} // NaN
    - [1, 2, 3] // NaN
    
    '5' + 1 // '51'
    '5' + true // "5true"
    '5' + false // "5false"
    '5' + {} // "5[object Object]"
    '5' + [] // "5"
    '5' + function (){} // "5function (){}"
    '5' + undefined // "5undefined"
    '5' + null // "5null"
    
    除了加法运算符有可能把运算子转为字符串，其他运算符都会把运算子自动转成数值（四则运算 排除加 加上求模）
    '5' - '2' // 3
    '5' * '2' // 10
    true - 1  // 0
    false - 1 // -1
    '1' - 1   // 0
    '5' * []    // 0
    false / '5' // 0
    'abc' - 1   // NaN
    10%"2" //0

## 转换为false的值
    undefined
    null
    0
    NaN
    ''
## 原始数据类型
   Undefined、Null、Boolean、Number、String、Symbol
   
## 引用数据类型
   对象、数组和函数
## typeof 返回的结果
   Undefined	"undefined"
   Null	"object" (见下方)
   Boolean	"boolean"
   Number	"number"
   String	"string"
   Symbol (ECMAScript 6 新增)	"symbol"
   函数对象 	"function"
   任何其他对象	"object"
  
## 其他
   ar numObj = 12345.6789;
   numObj.toFixed();         // 返回 "12346"：进行四舍五入，不包括小数部分
   numObj.toFixed(1);        // 返回 "12345.7"：进行四舍五入
   
   Math.ceil() 函数返回大于或等于一个给定数字的最小整数。(备注：Math.ceil() === 向上取整) //装天花板
   Math.ceil(.95);    // 1
   Math.ceil(4);      // 4
   Math.ceil(7.004);  // 8
   
   Math.floor() 返回小于或等于一个给定数字的最大整数。(备注：Math.floor() === 向下取整) //floor 地板
   Math.floor( 45.05); 
   // 45 
   Math.floor( 4 ); 
   // 4 
   Math.floor(-45.05); 
   // -46 

