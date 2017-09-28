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

###
## 其他
* [中文api](https://segmentfault.com/a/1190000008470355?utm_source=tuicool&utm_medium=referral)
* [ContentType](http://www.jianshu.com/p/0a5527422b1f)
    




