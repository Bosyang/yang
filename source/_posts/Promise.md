---
title: Promise 异步编程
date: 2018/11/26
---

# Promise

## 基本概念

* `Promise` 是异步编程的一种解决方案，比传统的 回调函数和事件 更合理更强大
* 所谓`Promis`，就是一个容器，里面保存这异步操作，从语法上说，`Promise`是一个对象，它可以获取异步操作的消息，`Promise` 提供统一的 API ，各种异步操作都可以用同样的方法进行处理。
* 有了`Promise` 对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回掉函数，此外，`Promise` 对象提供统一的接口，使得控制异步操作更加容易。
* `Promise` 也有一个缺点。首先，无法取消 `Promise`，一旦新建他就会立即执行，无法中途取消，其次，如果不设置回掉函数，`Promise` 内部抛出的错误，不会反应到外部，第三，当处于 `pending`状态时，无法得知目前进展到哪一个阶段

## 基本用法

ES6规定，`Promise` 对象是一个构造函数，用来生成 `Promise` 实例。

* 创造一个`Promise` 实例

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

* `Promise` 构造函数接收一个函数作为参数，该函数的两个参数分别为 `resolve` 和 `reject` ，它们是两个函数，有`JavaScript` 引擎提供，不用自己部署。
* `resolve` 函数的作用是，将`Promise`对象的状态从"未完成"变为"成功"(即从pending变为resolved)，在异步操作成功时调用，并将异步操作的结果，作为参数传递出啊去；`reject`函数的作用是，将`Promise`对象的状态从"未完成"变为"失败"(即从peding变为rejected)，在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。
* `Promise`实例生成后，可以用`then`方法分别指定`resolved`状态和`rejected`状态的回掉函数。

```js
promise.then(function(value) {
    // success
}, function(error) {
    // failure
});
```

* `then`方法可以接受两个回调函数作为参数，第一个回调函数是`Promise`对象的状态变为`resolved`时调用，第二个回调函数是`Promise`对象的状态变为`rejected`时调用，其中，第二个参数是可选的，不一定要提供。这两个函数都接收Promise对象传出的值作为参数。

Promise封装一个定时器

```JS
function sleep (time){
  return new Promise((resolve,reject)=>{
    setTimeout(resolve,time,'done')  //定时器第一个参数为回调函数，参数2:定时器时间，参数3 .....：回调函数的参数
  })
}
sleep(3000).then((value)=>{
  console.log(value);
})
```
* 上面代码中，`sleep`方法返回一个`Promise`实例，表示一段时间以后才会发生的结果。过了指定的时间（ms参数）以后，`Promise`实例的状态变为`resolved`，就会触发then方法绑定的回调函数。
