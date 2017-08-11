---
title: 关于页面文字处理
categories: [Css]
---
# 关于页面文字处理

## word-break是什么
normal 使用浏览器默认的换行规则,so,问题来了，什么是默认规则呢，空格换行，换行符换行  
break-all 充许单词内换行,也就是单词折行    
keep-all  只能在半角空格或连字符处换行。连字符(-)和空格换行
 
## word-wrap 是什么
normal	只在允许的断字点换行（浏览器保持默认处理）。短字点就是空格    
break-word	在长单词或 URL 地址内部进行换行。 单词折行

## white-space是什么
normal  连续的空白符会被合并，换行符会被当作空白符来处理。填充line盒子时，必要的话会换行    
nowrap   和 normal 一样，连续的空白符会被合并。但文本内的换行无效   
pre  连续的空白符会被保留。在遇到换行符或者<br>元素时才会换行。   
pre-wrap  连续的空白符会被保留。在遇到换行符或者<br>元素，或者需要为了填充line盒子时才会换行。   
pre-line  连续的空白符会被合并。在遇到换行符或者<br>元素，或者需要为了填充line盒子时会换行。 (除了换行符或者<br>其他和normal一样)    

## text-overflow是什么
clip 截断
ellipsis 省略号
<string> 字符串

## 其他
* [Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)



