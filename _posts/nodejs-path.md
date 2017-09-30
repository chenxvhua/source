---
title: path 模块
categories: [nodejs]
---
# path 模块
path 模块提供了一些工具函数，用于处理文件与目录的路径。可以通过以下方式使用
````
const path = require('path');
````
##Windows 与 POSIX
要想在posix和windows平台结果返回一致可以加上各自的前缀    
如：path.win32.basename('C:\\temp\\myfile.html')或者path.posix.basename('/tmp/myfile.html');
注意路径字符串带不带反斜杠可以结果会不一样如：fs.readdirSync('c:\\')与fs.readdirSync('c:') 

##方法
###path.basename(path[, ext])
返回路径中最后一部分   
注意:如果指定了ext,并且结果中包含ext,则省略ext,否则返回路径中的ext

````
console.log(path.basename('/foo/bar/baz/asdf/quux.html'))
//=>quux.html
console.log(path.basename('/foo/bar/baz/asdf/quux.html', '.html'))
//=>quux
console.log(path.basename('/foo/bar/baz/asdf/quux.html', '.txt'))
//=>quux.html
````

###path.dirname(path)
返回路径的目录
````
console.log(path.dirname('/foo/bar/baz/asdf/quux'));
//=>'/foo/bar/baz/asdf'
````
###path.extname(path)
返回 path 的扩展名，即从 path 最后一个 .（句号）字符到字符串结束,如果没有满足条件的，就返回空字符串
````
console.log(path.extname('index.coffee.md'));
//=>.md
````
###path.format(pathObject)
从一个对象返回一个路径字符串   
* 如果提供了 pathObject.dir，则 pathObject.root 会被忽略    
* 如果提供了 pathObject.base 存在，则 pathObject.ext 和 pathObject.name 会被忽略
````
var p=path.format({
    dir: '\\home\\user\\dir',
    base: 'file.txt'
});
//=>\home\user\dir\file.txt
````
###path.isAbsolute(path)
判定 path 是否为一个绝对路径
````
console.log(path.isAbsolute('/foo/bar'));//true
console.log(path.isAbsolute('C:\\baz'));//true
console.log(path.isAbsolute('./baz'));//false
console.log(path.isAbsolute('../baz'));//false
````

###path.join([...paths])
使用平台特定的分隔符把全部给定的 path 片段连接到一起，并规范化生成的路径
````
console.log(path.join('/foo', 'bar', 'baz/asdf', 'quux', '..'));
// 返回: '/foo/bar/baz/asdf'
````
###path.normalize(path)
规范化给定的 path，并解析 '..' 和 '.' 片段
````
console.log(path.normalize('/foo/bar//////baz\\\\asdf/quux////'));
//=>\foo\bar\baz\asdf\quux\
````
###path.parse(path)
返回一个对象，对象的属性表示 path 的元素
````
var obj= path.parse('/home/user/dir/file.txt');
console.log(JSON.stringify(obj));
//=>{"root":"/","dir":"/home/user/dir","base":"file.txt","ext":".txt","name":"file"}
````

###path.relative(from, to)
返回从 from 到 to 的相对路径（基于当前工作目录）
`````
var str=path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
console.log(str);
//=>..\..\impl\bbb
`````
###path.resolve([...paths])
会把一个路径或路径片段的序列解析为一个绝对路径
````
path.resolve('/foo/bar', '/tmp/file/');
// 返回: '/tmp/file'

path.resolve('wwwroot', 'static_files/png/', '../gif/image.gif');
// 如果当前工作目录为 /home/myself/node，
// 则返回 '/home/myself/node/wwwroot/static_files/gif/image.gif'
````

##属性
###path.delimiter
平台特定的路径分隔符    
window为;(分号)
POSIX为:(冒号)

###path.posix
path.posix 属性提供了 path 方法针对 POSIX 的实现
如 path.posix.parse() .....

###path.win32
path.win32 属性提供了 path 方法针对 Windows 的实现。
如 path.win32.parse() .....

###path.sep
平台特定的路径片段分隔符
* Windows 上是 \
* POSIX 上是 /

````
//var arr='foo/bar/baz'.split(path.sep);
//console.log(arr);
//=>[ 'foo/bar/baz' ]

//var arr='foo\\bar\\baz'.split(path.sep);
//console.log(arr);
//=>[ 'foo', 'bar', 'baz' ]
````








