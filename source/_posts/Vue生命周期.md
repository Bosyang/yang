# 生命周期

所有的生命周期钩子自动绑定 `this` 上下文到实例中，因此你可以访问数据，对属性和方法进行运算。这意味着**你不能使用箭头函数来定义一个生命周期方法** (例如 `created: () => this.fetchTodos()`)。这是因为箭头函数绑定了父上下文，因此 `this` 与你期待的 Vue 实例不同，`this.fetchTodos` 的行为未定义。

## 生命周期图示

下图展示了实例的生命周期。你不需要立马弄明白所有的东西，不过随着你的不断学习和使用，它的参考价值会越来越高。

<img src="https://cn.vuejs.org/images/lifecycle.png">

## [beforeCreate](https://cn.vuejs.org/v2/api/#beforeCreate)

- **类型**：`Function`

- **详细**：

  在实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=2964079374,2541441406&fm=173&app=25&f=JPEG?w=553&h=604&s=8271C730118FE14F44C540DA000080B2)

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=1426589767,3856573575&fm=173&app=25&f=JPG?w=522&h=312&s=C0411F74119ACDC80074F4CE030010B1)

我们在上面的例子中在的`beforeCreate`钩子中调用`Vue`的`data`和`method`，来看一下结果：

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=286215131,3982839788&fm=173&app=25&f=JPG?w=607&h=157&s=37FEEF36CF624D205C65BCFB03008035)

可以看到`Vue`中的`data`和方法都是去不到的，并且是在`wath`之前执行

## [created](https://cn.vuejs.org/v2/api/#created)

- **类型**：`Function`

- **详细**：

  在实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，`$el` 属性目前不可见。
  
* **主要应用：**调用数据，调用方法，调用异步函数

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=4249347146,621964453&fm=173&app=25&f=JPEG?w=640&h=586&s=C2718F70818FD14D1E54A8D20000C0B2)

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=1858455738,4278016&fm=173&app=25&f=JPG?w=639&h=244&s=8AF1CF148BC04C411A7590D00300D0B1)

结果：

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=3986693091,3912795656&fm=173&app=25&f=JPG?w=232&h=84&s=3AAA70239F204C0116DDA5DE000080B2)

可以看到：created钩子可以获取`Vue`的data，调用`Vue`方法，获取原本`HTML`上的直接加载出来的`DOM`，但是无法获取到通过挂载模板生成的`DOM`（例如：`v-for`循环遍历`Vue.list`生成`li`）

## [beforeMount](https://cn.vuejs.org/v2/api/#beforeMount)

- **类型**：`Function`

- **详细**：

  在挂载开始之前被调用：相关的 `render` 函数首次被调用。例如通过`v-for`生成的`html`还没有被挂载到页面上 （接 2`created`的代码）**该钩子在服务器端渲染期间不被调用。**

结果 beforeMount: 1

## [mounted](https://cn.vuejs.org/v2/api/#mounted)

- **类型**：`Function`

- **详细**：

  `el` 被新创建的 `vm.$el` 替换，并挂载到实例上去之后调用该钩子。如果 root 实例挂载了一个文档内元素，当 `mounted` 被调用时 `vm.$el` 也在文档内。

  注意 `mounted` **不会**承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 [vm.$nextTick](https://cn.vuejs.org/v2/api/#vm-nextTick) 替换掉 `mounted`：

  ```js
  mounted: function () {
    this.$nextTick(function () {
      // Code that will run only after the
      // entire view has been rendered
    })
  }
  ```

  **该钩子在服务器端渲染期间不被调用。**

（接 2`created`的代码）

结果 mounted: 3 可以看到到这里为止，挂载到实例上了，我们可以获取到`li`的个数了

## [beforeUpdate](https://cn.vuejs.org/v2/api/#beforeUpdate)

- **类型**：`Function`

- **详细**：

  数据更新时调用，发生在虚拟 DOM 打补丁之前。这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。

  **该钩子在服务器端渲染期间不被调用，因为只有初次渲染会在服务端进行。**

数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。 你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。 当我们更改`Vue`的任何数据，都会触发该函数

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=4099699163,4260093637&fm=173&app=25&f=JPG?w=453&h=99&s=C8718F50C5366C225CF8D943030050B1)

## [updated](https://cn.vuejs.org/v2/api/#updated)

- **类型**：`Function`

- **详细**：

  由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。

  当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态。如果要相应状态改变，通常最好使用[计算属性](https://cn.vuejs.org/v2/api/#computed)或 [watcher](https://cn.vuejs.org/v2/api/#watch) 取而代之。

  注意 `updated` **不会**承诺所有的子组件也都一起被重绘。如果你希望等到整个视图都重绘完毕，可以用 [vm.$nextTick](https://cn.vuejs.org/v2/api/#vm-nextTick) 替换掉 `updated`：

  ```js
  updated: function () {
    this.$nextTick(function () {
      // Code that will run only after the
      // entire view has been re-rendered
    })
  }
  ```

  **该钩子在服务器端渲染期间不被调用。**

数据更新就会触发（`vue`所有的数据只有有更新就会触发）,如果想数据一遍就做统一的处理，可以用这个，如果想对不同数据的更新做不同的处理可以用`nextTick`，或者是watch进行监听

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=745930405,12349775&fm=173&app=25&f=JPG?w=401&h=106&s=C0718F70C7347C234CF85953030070B1)

## [beforeDestroy](https://cn.vuejs.org/v2/api/#beforeDestroy)

- **类型**：`Function`

- **详细**：

  实例销毁之前调用。在这一步，实例仍然完全可用。

  **该钩子在服务器端渲染期间不被调用。**

## [destroyed](https://cn.vuejs.org/v2/api/#destroyed)

- **类型**：`Function`

- **详细**：

  Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不被调用。

  **该钩子在服务器端渲染期间不被调用。**

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=4136287011,766109910&fm=173&app=25&f=JPG?w=573&h=434&s=C0718F70111ED5CE4E719CDA0300C0B1)

结果：

可以看打到销毁`Vue`实例时会调用这两个函数

补充`$mount`

当你`vue`没有挂在el时，我们可以用`$mount`

![img](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=986075873,4272956589&fm=173&app=25&f=JPG?w=367&h=124&s=C0710F7087705C211C6494DA0300C0B1)

三.钩子的一些实战用法

1.异步函数

这里我们用定时器来做异步函数

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=3165699403,4051965807&fm=173&app=25&f=JPEG?w=640&h=558&s=8271C730910FC14D4E558CDA0000C0B2)

结果为：create: aaaaaaaa mounted: 3 created异步函数： 3 updated: 4 解释：可以看到因为是在created的钩子中加入异步函数，所以函数的执行顺序为： ceated钩子,mounted钩子,异步函数,updated钩子(根据事件队列原理,只有在updated后，li才是真的DOM渲染为4个，所以异步函数中获取的li的个数时是没有变化的li的个数)。 因为mounted获取到的是我们在Vue的data中设置初始值渲染的DOM，而我们是在异步函数中变化的list数据，所以mounted获取的li的个数为3。 update函数是只要数据vue绑定的数据变化就会触发，所以最后执行，为4

这是不是意味着可以直接在update函数中操作呢，其实不是，因为update函数是针对vue的所有数据的变化，而我们也有可能会有其他数据的变化。

例如下面的例子：

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=2169262960,1491226231&fm=173&app=25&f=JPEG?w=639&h=378&s=8871CF10155AE5CC547108DA000090B2)

结果为：

2.Vue.nextTick对异步函数的结果进行操作

我们想要改变数据时,各自触发各自的方法

![img](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=1971826948,3543434272&fm=173&app=25&f=JPEG?w=639&h=330&s=B284B54C1AEC816C0EF9E50F0000E0C3)

结果：

![img](https://ss0.baidu.com/6ONWsjip0QIZ8tyhnq/it/u=923951616,4153617320&fm=173&app=25&f=JPG?w=189&h=130&s=3EAA74230D5E40CA44F564DE0000C0B0)

 

 

我们可以看到通过$nextTick我们可以对异步函数的结果进行各自的操作