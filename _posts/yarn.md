---
title: 关于yarn介绍
categories: [other]
---
# 关于JavaScript数组你必须知道的几点

## 常用命令 
* yarn add命令  安装并且添加到package.json文件      
   参数讲解      
   --dev 保存到package.json中的 devDependencies      
   --peer 保存到package.json中的 peerDependencies      
   --optional 保存到package.json中的 optionalDependencies     
   默认保存到package.json中的 dependencies      
   --exact 死版本，1.0就是1.0     
   --tilde 小版本号可以动态    
* yarn remove命令 包名 或者加上--flag  移除指定包 
* yarn list --depth=0 显示级别是0的包信息
* yarn cache ls 显示所有缓存包
* yarn cache clean 或者包名，清理所有缓存的包，或则指定包
* yarn install 安装package.json文件中的包,  --force 强行安装所有包  --production 不会安装devDependencies下的包，其他的都会安装
    
    

## 其他
* [山寨中文api](https://yarn.bootcss.com/docs/cli/)
* [官方中文api](https://yarnpkg.com/zh-Hans/docs/cli/)



