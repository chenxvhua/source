---
title: process对象
categories: [nodejs]
---
# process对象

## 事件

###beforeExit     

当Node.js的事件循环数组已经为空，并且没有额外的工作被添加进来，事件'beforeExit'会被触发  
   
```
process.on('beforeExit', (code) => {
      console.log(`About to exit with code: ${code}`);
});
//=> About to exit with code: 0
```

###disconnect

如果Node.js进程是由IPC channel的方式创建的(see the Child Process and Cluster documentation)，
当IPC channel关闭时，会触发'disconnect'事件

###exit

Node.js进程即将结束

```
process.on('exit', (code) => {
    console.log(`About to exit with code: ${code}`);
});
//=> About to exit with code: 0
```


###message
如果Node.js进程是由IPC channel的方式创建的(see the Child Process， and Cluster documentation)，
当子进程收到父进程的的消息时(消息通过childprocess.send()发送）， 会触发'message'事件。

```

```
###rejectionHandled
如果未处理的reject随后又添加了catch处理，会触发rejectionHandled，见代码
```
var p = Promise.reject(new Error('WTF'));
setTimeout(function() {
    console.log('before hello');
    p.catch(function() {
        console.log('hello');
    });
}, 1000);

process.on('unhandledRejection', function() {
    console.log('[unhandledRejection]');
});

process.on('rejectionHandled', function() {
    console.log('[rejectionHandled]');
});

//=>[unhandledRejection]
//=>before hello
//=>[rejectionHandled]
//=>hello

```
###uncaughtException
如果有未捕获的异常，进程会退出，后续代码不继续运行，然而添加了uncaughtException监听，就不会中断程序

```
process.on('uncaughtException', (err) => {
    console.log(`Caught exception: ${err}\n`);
});

setTimeout(() => {
    console.log('This will still run.');
}, 500);

// 故意调用一个不存在的函数，应用会抛出未捕获的异常
nonexistentFunc();
console.log('This will not run.');
```
###unhandledRejection
如果Promise调用了reject，并且没有做异常处理，会触发unhandledRejection
```
var p=Promise.reject();
process.on('unhandledRejection', (reason, p) => {
    console.log('unhandledRejection');
});

```
###warning
Process发出的警告
```
process.emitWarning('Something happened!');
process.on('warning', (warning) => {
    console.warn("name",warning.name);
    console.warn("message",warning.message);
    console.warn("stack",warning.stack);
});
//=>name Warning
//=>   message Something happened!
//=>    stack Warning: Something happened ....
```
###Signal Events
各种信号事件
```
process.on('SIGWINCH', () => {
    console.log('Received SIGINT.  Press Control-D to exit.');
});
//=>Received SIGINT.  Press Control-D to exit
```

## 方法
###process.abort()
使Node.js进程立即结束，并生成一个core文件
```
process.abort();
//=>1: node::Abort() [/Users/chenxuhua/.nvm/versions/node/v8.4.0/bin/node]
//=>2: node::Chdir(v8::FunctionCallbackInfo<v8::Value> const&) [/Users/chenxuhua/.nvm/versions/node/v8.4.0/bin/node]
```
###process.chdir(directory)
变更Node.js进程的当前工作目录，如果变更目录失败会抛出异常
```
console.log(`Starting directory: ${process.cwd()}`);
try {
    process.chdir('/tmp2222');
    console.log(`New directory: ${process.cwd()}`);
} catch (err) {
    console.error(`chdir: ${err}`);
}

//=>Starting directory: /Users/chenxuhua/pure
//=>chdir: Error: ENOENT: no such file or directory, uv_chdir
```
###process.cpuUsage
上一次调用process.cpuUsage()方法的结果，可以作为参数值传递给此方法，得到的结果是与上一次的差值

````
const startUsage = process.cpuUsage();
// { user: 38579, system: 6986 }

// spin the CPU for 500 milliseconds
const now = Date.now();
while (Date.now() - now < 500);

console.log(process.cpuUsage(startUsage));
// { user: 514883, system: 11226 }
````

###process.cwd()
process cwd() 方法返回 Node.js 进程当前工作的目录

````
console.log('Current directory: ${process.cwd()}');
//=>Current directory: /Users/chenxuhua/pure
````

###process.disconnect()
允许子进程一旦没有其他链接来保持活跃就优雅地关闭
调用process.disconnect()的效果和父进程调用ChildProcess.disconnect()的一样,

###process.emitWarning(warning[, options])
可用于发出定制的或应用特定的进程警告
````
process.emitWarning('Something happened!', {
    code: 'MY_WARNING',
    detail: 'This is some additional information'
});

process.on('warning', (warning) => {
  console.warn(warning.name.message);    
  console.warn(warning.name.code);   
  console.warn(warning.name.detail);  
});

//=>Something happened!
//=>MY_WARNING
//=>This is some additional information
````
###process.exit()
在所有'exit'事件监听器都被调用了以后，终止进程
````
process.exitCode="这里是退出code";
process.on('exit', (code) => {
    console.log(`About to exit with code: ${code}`);
});
process.exit();
//=>About to exit with code: 这里是退出code
````
###process.getegid()
有效数字标记的组身份    
注意：只在POSIX平台有效

###process.getgid()
数字标记的组身份
注意：只在POSIX平台有效

###process.getgroups()
返回数组，其中包含了补充的组ID
注意：只在POSIX平台有效

###process.geteuid()
有效数字标记的用户身份
注意：只在POSIX平台有效


###process.getuid()
数字标记的用户身份
注意：只在POSIX平台有效

###process.hrtime([time])
都是相对于过去某一时刻的值，与一天中的时钟时间没有关系，因此不受制于时钟偏差。    
此方法最主要的作用是衡量间隔操作的性能
````
const time = process.hrtime();
setTimeout(() => {
    const diff = process.hrtime(time);
    console.log(`Benchmark took ${diff[0]  +"="+ diff[1]} nanoseconds`);
    // benchmark took 1000000552 nanoseconds
}, 1000);
````
###process.initgroups(user, extra_group)
读取/etc/group文件，并且初始化组访问列表      
注意：这个函数只在POSIX平台有效

###process.kill(pid[, signal])
signal发送给pid标识的进程

###process.memoryUsage()
返回Node.js进程的内存使用情况的对象，该对象每个属性值的单位为字节
heapTotal 和 heapUsed 代表V8的内存使用情况。
external代表V8管理的，绑定到Javascript的C++对象的内存使用情况

````
console.log(process.memoryUsage());
//=>{
      rss: 4935680,
      heapTotal: 1826816,
      heapUsed: 650472,
      external: 49879
    }
````

###process.nextTick(callback[, ...args])
这种方式不是setTimeout(fn, 0)的别名。它更加有效率。事件轮询随后的ticks 调用，会在任何I/O事件（包括定时器）之前运行

````
console.log('start');
process.nextTick(() => {
    console.log('nextTick callback');
});
setTimeout(function () {
   console.log("这里是回调函数");
},0)
console.log('scheduled');
//=>start
//=>scheduled
//=>nextTick callback
//=>这里是回调函数
````

###process.send(message[, sendHandle[, options]][, callback])
子进程给父进程发消息

###process.setegid
设置A group name or ID
注意：只在POSIX平台有效

###process.seteuid(id)
设置A user name or ID
注意：只在POSIX平台有效

###process.setgid(id)
设置The group name or ID
注意：只在POSIX平台有效

###process.setgroups
设置 groups
注意：只在POSIX平台有效

###process.setuid
设置uid
注意：只在POSIX平台有效

###process.umask
创建掩码

###process.uptime()
进程运行时间秒长,单位为秒
````
setTimeout(function () {
    console.log(process.uptime());
},1000)

````

## 属性
###process.arch
返回一个标识Node.js在其上运行的处理器架构的字符串。例如 'arm', 'ia32', or 'x64'.
```
console.log(process.arch);
//=>x64
```
###process.argv
process.argv 属性返回一个数组   
argv[0]==process.execPath
argv[1]==当前执行的JavaScript文件路径
...argv其他命令行参数
```
命令行输入 node server.js a b c

process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});
//=>0: /Users/chenxuhua/.nvm/versions/node/v8.4.0/bin/node
//=>1: /Users/chenxuhua/pure/server.js
//=>2: a
//=>3: b
//=>4: c
```
###process.argv0
process.argv0属性，保存Node.js启动时传入的argv[0]参数值的一份只读副本

###process.channel
process.channel属性保存IPC channel的引用

###process.config
返回一个Javascript对象,此对象描述了配置项信息。注意： process.config属性值不是只读的
````
process.config.abc="测试";
console.log(process.config);
//==>....want_separate_host_toolset_mkpeephole: 0,
//==>xcode_version: '7.0' },
//==>abc: '测试' }
````
###process.connected
process.connected如果为false，则不能通过IPC channel使用process.send()发送信息

###process.env
环境信息的对象，可读可写    
注意：在Windows系统下，环境变量是不区分大小写的

###process.execArgv
返回Node.js特定的命令行选项
````
node --harmony index.js --version
console.log("process.execArgv="+JSON.stringify(process.execArgv));
console.log("process.argv="+JSON.stringify(process.argv));
//=>process.execArgv=["--harmony"]
//=>process.argv=["C:\\Program Files\\nodejs\\node.exe","C:\\Users\\chenxuhua\\Desktop\\react-study\\nodejs\\index.js","--version"]
````

###process.execPath
返回node.exe执行路径
````
console.log("process.execPath="+process.execPath);
//=>C:\\Program Files\\nodejs\\node.exe
````
###process.mainModule
process.mainModule属性提供了一种获取require.main的替代方式

````
console.log("process.mainModule="+JSON.stringify(process.mainModule));
console.log("require.main="+JSON.stringify(require.main));
//=>输出相同
````

###process.platform
返回字符串，标识Node.js进程运行其上的操作系统平台。 例如'darwin', 'freebsd', 'linux', 'sunos' 或 'win32'

###process.release
版本发布信息
````
console.log(process.release);
//=>{ name: 'node',
  lts: 'Boron',
  sourceUrl: 'https://nodejs.org/download/release/v6.11.0/node-v6.11.0.tar.gz',
  headersUrl: 'https://nodejs.org/download/release/v6.11.0/node-v6.11.0-headers.tar.gz',
  libUrl: 'https://nodejs.org/download/release/v6.11.0/win-x64/node.lib' }

````

###process.stderr
返回连接到stderr(fd 2)的流

###process.stdin
返回连接到stdin(fd 0)的流
````
process.stdin.setEncoding('utf8');
process.stdin.on('readable', () => {
    const chunk = process.stdin.read();
    if (chunk !== null) {
        process.stdout.write(`这里是控制台输入的内容: ${chunk}`);
    }
});

process.stdin.on('end', () => {
    process.stdout.write('end');
});
//控制台输入1回车
//=>这里是这里是控制台输入的内容:1
````
###process.stdout
返回连接到 stdout (fd 1)的流
````
//如输入即输出
process.stdin.pipe(process.stdout);

//列2
/*1:声明变量*/
var num1, num2;
/*2：向屏幕输出，提示信息，要求输入num1*/
process.stdout.write('请输入num1的值：');
/*3：监听用户的输入*/
process.stdin.on('data', function (chunk) {
    if (!num1) {
        num1 = Number(chunk);
        /*4：向屏幕输出，提示信息，要求输入num2*/
        process.stdout.write('请输入num2的值');
    } else {
        num2 = Number(chunk);
        process.stdout.write('结果是：' + (num1 + num2));
    }
});

````
###process.title
返回标题

###process.version
返回一个对象，此对象列出了Node.js和其依赖的版本信息
````
console.log(process.versions);
//=>
{
  http_parser: '2.3.0',
  node: '1.1.1',
  v8: '4.1.0.14',
  uv: '1.3.0',
  zlib: '1.2.8',
  ares: '1.10.0-DEV',
  modules: '43',
  icu: '55.1',
  openssl: '1.0.1k',
  unicode: '8.0',
  cldr: '29.0',
  tz: '2016b' }
````

## 其他
###Exit Codes列表
* 0.Node.js正常退出
* 1.未捕获致命异常
* 2 - 未使用
* 3内部JavaScript解析错误 
* 4内部JavaScript评估失败 
* 5致命错误
* 6非功能内部异常处理程序 - 有一个未捕获的异常，但内部致命异常处理函数以某种方式设置为非函数，无法调用。
* 7内部异常处理程序运行时失败 - 有一个未捕获的异常，内部致命异常处理函数本身在尝试处理它时抛出一个错误。这可能会发生
* 8 - 未使用在以前版本的Node.js中，退出代码8有时表示未捕获的异常。
* 9-无效的参数 - 指定了一个未知的选项，或者提供了一个没有值的需求值的选项。
* 10内部JavaScript运行时失败 
* 12调试参数无效 
* 128信号退出 

    




