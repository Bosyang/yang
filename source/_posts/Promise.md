---
title: Promise 异步编程
date: 2018/11/26
---

# Promise

## 基本概念

* Promise 是异步编程的一种解决方案，比传统的 回调函数和事件 更合理更强大
* 所谓Promis，就是一个容器，里面保存这异步操作，从语法上说，Promise是一个对象，它可以获取异步操作的消息，Promise 提供统一的 API ，各种异步操作都可以用同样的方法进行处理。
* 有了Promise 对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回掉函数，此外，Promise 对象提供统一的接口，使得控制异步操作更加容易。
* Promise 也有一个缺点。首先，无法取消 Promise，一旦新建他就会立即执行，无法中途取消，其次，如果不设置回掉函数，Promise 内部抛出的错误，不会反应到外部，第三，当处于 pending状态时，无法得知目前进展到哪一个阶段

## 基本用法

ES6规定，Promise 对象是一个构造函数，用来生成 Promise 实例。

* 创造一个Promise 实例

```js
comst promise = new Promise(function(resolve,reject) {
     // ... some code
    if(/* 异步操作成功*/){
       resolve(value)
       }else{
           reject(error)
       }
})
```

