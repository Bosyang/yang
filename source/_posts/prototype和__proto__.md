---
title: prototype和__proto__、constructorp
date: 2018/11/14
---

## prototype 和 __ proto __ 的关系是什么

* prototype和 __ proto __ 都指向原型对象，任意一个函数（包括构造函数）都有一个prototype属性，指向该函数的原型对象，同样任意一个构造函数实例化的对象，都有一个 __ proto __ 属性（ __ proto __ 并非标准属性，ECMA-262第5版将该属性或指针称为[[Prototype]]，可通过Object.getPrototypeOf()标准方法访问该属性），指向构造函数的原型对象。 
* 实例对象通过 __ proto __ 找到 原型对象 
* 原型对象 通过 constructor 找到 构造函数
* 构造函数 通过 prototype 找到 原型对象
* 构造函数 通过实例化 创建 实例对象

##  拓展

### 构造函数

* 在 JavaScript 中，用 new 关键字来调用的函数，称为构造函数。构造函数首字母一般大写 
* 构造函数创建对象,也可叫做实例化
*  当一个函数创建好以后，我们并不知道它是不是构造函数，即使像上面的例子一样，函数名为大写，我们也不能确定。只有当一个函数以 new 关键字来调用的时候，我们才能说它是一个构造函数 

``` js
// 构造函数
function Dog (food) {
    this.food = food
    onBark = function () {
        console.lo('bark!')
    }
}
var dog = new Dog('bone') //实例化对象
Dog.prototype === dog.__proto__
//每一个对象都有原型(prototype)属性，构造函数Dog的原型属性指向Dog的原型对象，而实例dog的原型([[prototype]])属性也指向原型对象
```

### 原型对象

*  我们创建的每一个函数都有prototype属性，它指向一个对象，即原型对象。原型对象包含这个特定类型所有实例共享的属性和方法，所以原型对象可以理解为这个特定类型构造函数的实例。 
*  JS 创建的对象都有一个 __ proto __ 属性， __ proto __ 属性连接实例和构造函数的原型对象，对外不可见，无法直接获得，可以通过Object.getPrototypeOf（）方法得到这个属性 

###  原型链

* Javascript 是面向对象的，每个实例对象都有一个 __ proto __ 属性，该属性指向它原型对象，这个实例对象的构造函数有一个原型属性 prototype，与实例的 __ proto __ 属性指向同一个对象。当一个对象在查找一个属性的时，自身没有就会根据 __ proto __ 向它的原型 进行查找，如果都没有，则向它的原型的原型继续查找，直到查到Object.prototype. __ proto __ 为 null，这样也就形成了原型链

### __ proto __

* __ proto __ 是JavaScript 中 所谓的原型
  *  构造函数的 __ proto __ 的属性指向 function() 
  * 对象字面量的 __ proto __ 的属性指向 Object
  * 数组的 __ proto __ 的属性指向 Array[0]

