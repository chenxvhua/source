---
title: 关于正则表达式介绍
categories: [other]
---
# 关于正则表达式介绍

## 正则表达式中的特殊字符
* (?:x) 表示匹配但是不记住，比如/(?:a)c/表示匹配ac
*  (?=x) 表示后面必须跟着x，但是x又不在匹配结果中
*  (?!x) 表示后面必须不跟着x，但是x又不在匹配结果中
*  [xyz] 只要表示字符都可以在里面比如\d \w 
*  [\b] 匹配一个退格(U+0008)
* \b和\B \b匹配单词边界包括头尾,\B非单词边界
* \d和\D \d匹配数字,\D匹配非数字
* \w和\W \w（字母、数字或者下划线）, \W匹配（字母、数字或者下划线）
* \s和\S \s匹配空格等，\S匹配除空格等之外的任意字符
    
## JS正则作用
* exec	如果匹配成功，exec() 方法返回一个数组，并更新正则表达式对象的属性。
返回的数组将完全匹配成功的文本作为第一项，将正则括号里匹配成功的作为数组填充到后面。
     
* test	一个在字符串中测试是否匹配的RegExp方法，它返回true或false。
* match	
    如果正则表达式没有 g 标志，则 str.match() 会返回和 RegExp.exec() 相同的结果。
    而且返回的 Array 拥有一个额外的 input 属性，该属性包含被解析的原始字符串。
    另外，还拥有一个 index 属性，该属性表示匹配结果在原字符串中的索引（以0开始）。
    
    如果正则表达式包含 g 标志，则该方法返回一个 Array ，
    它包含所有匹配的子字符串而不是匹配对象。
    捕获组不会被返回(即不返回index属性和input属性)。如果没有匹配到，则返回  null 。
    也就是说只包括结果,如下
            var str="111a222b33"
            var re = /\d+/g;   
            
            var found =str.match(re);  
            //console.log(JSON.stringify(found));  
            console.log(found);
            //"111,222,33"

  
    search	一个在字符串中测试匹配的String方法，它返回匹配到的位置索引，或者在失败时返回-1。
    replace	一个在字符串中执行查找匹配的String方法，并且使用替换字符串替换掉匹配到的子字符串。
    split	一个使用正则表达式或者一个固定字符串分隔一个字符串，并将分隔后的子字符串存储到数组中的String方法。
    
    
    
    
    

## 其他
* [Array](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)



