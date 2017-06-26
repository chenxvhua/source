---
title: Vue中Data、Computed,Methods 使用总结
categories: [Vue]
---
#  Vue中data、computed,methods 使用总结

## Data

> 对象必须是纯粹的对象(键值数据)  
> vm.$data 访问原始数据对象 
> 以 _ 或 $ 开头的属性 不会 被 Vue 实例代理,你可以使用例如 vm.$data._property 的方式访问这些属性。

## Computed
> 所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例  
> 计算属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。  

## methods
> this 自动绑定为 Vue 实例。

## watch

    watch: {
      a: function (val, oldVal) {
        console.log('new: %s, old: %s', val, oldVal)
      },
      // 方法名
      b: 'someMethod',
      // 深度 watcher
      c: {
        handler: function (val, oldVal) { /* ... */ },
        deep: true
      }
    }





