---
title: Markdown 使用总结
categories: [other]
---
# Markdown 使用总结

## 段落和换行
段落:前面留个空行  
换行：在末尾敲连个空格

## 标题
标题类似h1~h6敲#来模拟

## 区块引用
>这里是引用 就>表示

## 列表
* 这里是列表1
* 这里是列表2
1. 这里是列表1
2. 这里是列表1

可以看出是通过*来模拟无序列表，数字加一个英文句点，来模拟有序列表

## 代码区块
     var a=0;
     alert(a);
     
上面就是代码块，通过敲4个空格来实现
     
## 分隔线
通过---来实现
---

## 链接
这个是 [百度](http://www.baidu.com/ "标题") 行内链接

## 强调
*这里是em强调* **这里是strong强调**  

强调有两个级别，用星号（*）来模拟

## 代码
`<div>这里是测试</div>`

代码是通过反引号来模拟，可以自动转化html实体

## 图片

![图片替代文字](https://www.baidu.com/img/bd_logo1.png "图片标题")

图片和链接差不多，只是前面加了个感叹号


## 反斜杠

\\   反斜线  
\`   反引号  
\*   星号  
\_   底线  
\{}  花括号  
\[]  方括号  
\()  括弧  
\#   井字号  
\+   加号  
\-   减号  
\.   英文句点  
\!   惊叹号   

这些需要加上反斜杠才能做普通字符显示

## 自动链接
<http://www.baidu.com/>

通过尖括号里面放入链接来实现
