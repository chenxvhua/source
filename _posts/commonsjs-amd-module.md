---
title: amd、commonjs, es6模块使用介绍
categories: [JavaScript]
---
#amd、commonjs, es6模块使用介绍

## amd
###定义amd模块
define(function (require, exports, module) {
    console.log("one");
    function  myName() {
        console.log("张三");
    }

    function  myHobby() {
        console.log("爬山");
    }

    function  myAddress() {
        console.log("xx路");
    }
    module.exports={
        "myName":myName,
        "myHobby":myHobby,
    }
});
###使用amd模块
    require(['./one.js', './two.js'], function (one,two){
                        one.myName();
                        //two.myAddress();
    });


## commonjs
###定义commonjs模块
    function showName() {
        console.log("这里是执行showName");
    }
    module.exports={
         showName:showName
    }
###使用commonjs模块
    var r=require("one");
    r.showName();

##es6
###定义es6模块
    export function showName() {
        console.log("这里是执行showName");
    }
###使用es6模块
 export { showName } from './one.js';
 showName();
 
##webpack

Webpack具有requireJs和browserify的功能，对 CommonJS 、 AMD 、ES6的语法做了兼容

## requireJs的require和 webpack的require.ensure
###requireJs
	require(['./one.js', './two.js'], function (one,two){
					 //one.myName();
					//two.myAddress();
	});
	
one.js和two.js代码会执行

###webpack的require.ensure

    require.ensure(['./one.js', './two.js'], function (one,two){
					 //one.myName();
					//two.myAddress();
	});
one.js和two.js会下载，但代码没有执行




