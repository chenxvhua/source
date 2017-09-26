---
title: es6 模块使用介绍
categories: [JavaScript]
---
#es6 模块使用介绍

## 输出接口export
* 输出变量 export var i=0
* 输出方法 export function showName(){}
* 输出类export class nameClass {}
* 一次性输出多个 export {xx,bb,cc}
* 重命名输出 export {xx as yy} 只能通过这种方式重命名

## 输入接口import
* 输入默认接口(注意没有大括号) import varName(变量名随便定义) from "./xx.js" 
* 输入n个接口(注意有大括号) import {varName1,varName2,...} from "./xx.js" 
* 输入接口另起名 import {varName1 as otherName1,varName2 as otherName2,...} from "./xx.js" 
* 同时输入默认接口和非默认接口(注意顺序) import_(变量名随便定义), {varName1 as otherName1,varName2 as otherName2,...} from "./xx.js" 
* 模块整体加载(注意没有大括号) import * as g from "./xx.js" 

##export 与 import 的复合写法
* 输出默认接口 export { default } from './xx.js'
* 接口改名 export { foo as myFoo } from './xx.js'
* 整体输出 export * from './xx.js'
* 具名接口改为默认接口 export { es6 as default } from './xx.js'
* 默认接口改名为具名接口 export { default as es6 } from './xx.js'




