# Typescript

## 安装

前提先按node

```bash
npm install -g typescript
```

写文件  `xxx.ts`

运行生成 js 文件

```bash
tsc greeter.ts
```



## VScode 自动生成 js 文件

1. 先生成一个 `tsconfig.json`

2. 当前项目 目录下 运行

```bash
tsc --init
```

3. 在 tsconfig.json 文件中 配置

   `outDir` ts 文件生成路径

4. 在菜单栏 终端 中选择 运行任务 

   搜索 tsc 监视 tsconfig.json

5. 保存 ts 文件 自动生成到 js 文件夹



## 数据类型

### 数字类型(number)

### 布尔类型(boolean)

###  字符串(string)

### 数组(Array)

在定义时 规定了类型 无法再改变

* ts 中定义数组 有 两种 方式

1. 第一种定义数组的方式

 ```js
      var arr : number [ ] = [11, 22 , 33]
      console.log( arr ) // [11, 22 , 33]
      // 定义时 规定了数组内部 的 数据类型为number 当改为其他类型时 会报错
 ```

2. 第二种定义数组的方式

```js
var arr : Array<number> = [11, 22, 33]
console.log( arr ) // [11, 22, 33]
```

### 元组类型(tuple)

1. 也属于数组类型

```js
let arr : [ number , string  ] = [123, 'this is ts']
console.log( arr ) //  [123, 'this is ts']
```

### 枚举类型(enum)

1. `enum`类型是对JavaScript标准数据类型的一个补充。 像C#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。

```js
enum Flag ={ success = 1 , error = 2 }
let f : Flag.success
console.log( f )    //  1
```

2.  

```js
enum Color { blue , red , 'orange'}
var c : Color = Color.red
console.log( c )     //  1  如果标识符没有赋值 他的值就是下标
```

3.  

```js
enum Color { blue , red = 3 , 'orange'}
var c : Color = Color.orange
console.log( c )     //  4   改变下标
```

4.  

```js
enum Error { 'underfined ' = -1 , 'null' = 2 ,'success' = 1}
var e : Error = Erro.null
console.log( e )      // 1  
```

### 任意类型(Any)

```js
var num : number = 123 ;
num = 'str'   //  报错

var  a : any = 123 ;
num = true ;
console.log( num )  // true 
```

1. 实际操作中用法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <div id="box">
        box
    </div>
    <script src="js/hello world.js"></script>
</body>
</html>
```

```js
 var box : any = document.getElementById('box') // box要指定为any 类型 
 box.style.color = 'red'  //否则 会 报错
```

### void类型

1. 

```js
// es5 定义方法
function run ( ){
    console.log('run')
}
run()
```

2. 

```js
//表示方法没有返回 任何类型
function run ( ) : void {
    console.log('run')
}
run()
```

3. 

``` js
function run ( ) : number {    //错误写法   
    console.log('run')
}
run()
```

4. 

```js
function run ( ) : number {    // 如果有返回值 要写返回值类型   正确写法
    return 123
}
run()
```

### null 和 undefined

1. 

```js
var num : number    // 定义没有赋值 会报错
console.log( num )  
```

2. 

```js
var num : number | undefined
num = 123
console.log( num ) //输出123
```

3. 

```js
var num : number | undefined   // 定义没有赋值 不会报错
console.log( num ) // 输出 ： undefined     //正确
```

4. 一个元素 可能是 number 可能是 null 可能是 undefind   一个元素可以设置多个类型

```js
var num : number | null | undefined
num = 1234
console.log( num )   // 输出1234
```



### never类型

1. 代表从不会出现的值 

2. 

```js
var a : undefined;
a = null // 报错
var b : null
b = null //正确写法
```

3. 

```js
var a : never
a = 123   //报错
```

4. 

```js
var a : never
a= (()=>{
     throw new Error( '错误' )
})()
```

### Object

**Object ：**`object`表示非原始类型，也就是除`number`，`string`，`boolean`，`symbol`，`null`或`undefined`之外的类型。

使用`object`类型，就可以更好的表示像`Object.create`这样的API

```js
declare function create(o: object | null): void;

create({ prop: 0 }); // OK
create(null); // OK

create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
```



## 类型校验

* 写`typescript`代码必须指定类型

```js
var flag: boolean = true
flag = 123 // 报错
flag = false  
console.log( flag )  // 输出 false
```

 ```js
var num : number = 123
num = 456 
console.log( num ) // 输出456
num = 'str'  //报错
 ```



## TypeScript函数

1. 函数定义

```js
// es5 定义函数方法
function run ( ) {
    return 'run'
}
var run2 = function( ) [
    return 'run2'
]
```

```js
// ts 中定义函数方法
function run ( ) : string {
    return 123;    // 报错   声明了 返回为 字符串
}
function run2 ( ) : string {
    return 'run2';    // 正确
}


// 匿名函数
var fun2 = function ( ) : number {
    return 123 
}
fun2 ( )   


//ts 中 定义方法传参 
function getInfo ( name : string , age : number ) : string{
    return `${name} --- ${age}`
}
alert( getInfo ( 'zhangsan' , '20'))         // 报错
alert( getInfo ( 'zhangsan' , 20))        // 返回值 有类型 参数也要规定类型


// ts匿名函数定义
var getInfo = function ( ) ( name : string , age : number ) : string{
    return `${name} --- ${age}`
}
alert( getInfo ( 'zhangsan' , 40))   


//没有返回值的方法
var function run : void ( ) {
    console.log('run')
}
run ( )   // 打印出  run
```

2. 方法可选参数

* ES5 里面 方法的 形参和实参 可以不一样 ，但 ts 中必须一样， 如果不一样就要配置参数  
* 用 问号 `?` 配置可选参数
* 注意 可选参数 必须配置到参数的最后面

```js
function getInfo ( name : string , age : number ) : string{
    if ( age ) {
        return `${name} --- ${age}`
    }else {
        return `${name} --- 年龄保密`
    }
}
alert( getInfo ( 'zhangsan' ))    // 可执行 但是 编译报错

// 用  ？  配置 可选参数   
function getInfo ( name : string , age ? : number ) : string{
    if ( age ) {
        return `${name} --- ${age}`
    }else {
        return `${name} --- 年龄保密`
    }
}
alert( getInfo ( 'zhangsan' ))    //  ? 配置 可选参数
```

3. 默认参数

* es5里面没法设置默认参数，es6和 ts 中可以设置默认参数

```js
function getInfo ( name : string , age : number = 20 ) : string{
    if ( age ) {
        return `${name} --- ${age}`
    }else {
        return `${name} --- 年龄保密`
    }
}
alert( getInfo ( 'zhangsan' ))    //  zhangsan --- 30
```

4. 剩余参数

* 

```js
function sum ( a : number , b : number , c : number , d : number ) : number {
    return a + b + c + d
}
alert( sum ( 1 , 2 , 3 , 4 ))
```

* 三点运算符

```js
//  三点运算符接收 传过来的参数
function sum ( ...result : number [ ] ) : number {
    var sum = 0 
    for ( var i = 0 ; i < result.length ; i++ ) {
        sum += result [ i ]
    }
    return sum 
}
alert( sum ( 1 , 2 , 3 , 4 ))
```

5. 函数重载

* ts 为了 兼容 es5 以及 es6 重载的写法  和  Java 中 有区别

```js
function css ( config : any ) : any {
    
}
function css ( config : any , value : ) ;
//es5 中 出现同名的方法 。下面的方法 会替换上面的方法

// ts 中的重载
function getInfo ( name : string ) : string
function getInfo ( age : number ) : number
function getInfo ( str : any ) : any {
    if ( typeof str === 'string' ) {
        return '我叫： ' + str
    }else{
        return '我的年龄是' + str
    }
}
function getInfo(name:string):string;
function getInfo(name:string,age:number):string;
function getInfo(name:any,age?:any):any{
    if(age){
      return '我叫：'+name+'我的年龄是'+age;
    }else{
      return '我叫：'+name;
    }
}
```

6. 箭头函数  

* this 指向   箭头函数里面this指向上下文

```js
setTimeout(function(){

   alert('run')
 },1000)

↓  ↓  ↓  
//es6
        setTimeout(()=>{

            alert('run')
        },1000)
    
```

## typescript中的类

### es5中的类

1. es5 中 没有专门定义类的方法

```js
function Person( ) {
    this.name = '张三',
    this.age = 20
}
var p = new Person( )
alert( p.name )
```

2. 构造函数和原型链增加方法

```js
function Person( ) {
    this.name = '张三',
    this.age = 20
    //构造函数定义
    this.run = function( ){
        alert( this.name + '再运动')
    }
}
//原型链定义   原型链上的属性会被多个实例共享  构造函数不会
Person.prototype.sex = '男'
Person.prototype.work = function( ) {
    alert( this.name + '在工作' )
}
var p = new Person( )
//alert( p.name )
p.run( )
p.work( )
```

3. 类里面的静态方法

```js
function Person( ) {
    this.name = '张三',
    this.age = 20
    //构造函数定义
    this.run = function( ){
        alert( this.name + '再运动')
    }
}
//添加静态方法
Person.getInfo = function( ) {
    alert( '这是静态方法' )
}
//原型链定义   原型链上的属性会被多个实例共享  构造函数不会
Person.prototype.sex = '男'
Person.prototype.work = function( ) {
    alert( this.name + '在工作' )
}
var p = new Person( )
//alert( p.name )
p.run( )
p.work( )
//静态方法调用
Person.getInfo( )
```

4. es5 中的继承

```js
function Person( ) {
    this.name = '张三',
    this.age = 20
    //构造函数定义
    this.run = function( ){
        alert( this.name + '在运动')
    }
}
//原型链定义   原型链上的属性会被多个实例共享  构造函数不会
Person.prototype.sex = '男'
Person.prototype.work = function( ) {
    alert( this.name + '在工作' )
}
//原型链 + 对象冒充的组合继承方式
function Web( ) {
    Person.call( this )    //对象冒充实现继承
}

var w = new Web( )
w.run( )   //张三在运动    //对象冒充 可以继承 构造函数里面的属性和方法
w.wort( )    // 对象冒充 可以继承构造函数里面的属性和方法  但是没法继承原型链上面的属性和方法
```

```js
//原型链 实现继承
function Person( ) {
    this.name = '张三',
    this.age = 20
    //构造函数定义
    this.run = function( ){
        alert( this.name + '在运动')
    }
}
//原型链定义   原型链上的属性会被多个实例共享  构造函数不会
Person.prototype.sex = '男'
Person.prototype.work = function( ) {
    alert( this.name + '在工作' )
}
//原型链 + 对象冒充的组合继承方式
function Web( ) {

}
Web.prototype = new Person( )  //原型链 实现继承
var w = new Web( )
w.run( )
w.work( )  //   原型链实现继承 既可以 继承构造函数内的属性和方法，也可以继承原型链上的属性和方法
```

```js
//原型链实现继承的问题
function Person(name, age ) {
    this.name = name
    this.age = age
    //构造函数定义
    this.run = function( ){
        alert( this.name + '在运动')
    }
}
//原型链定义   原型链上的属性会被多个实例共享  构造函数不会
Person.prototype.sex = '男'
Person.prototype.work = function( ) {
    alert( this.name + '在工作' )
}

function Web ( name , age  ) {
    
}
Web.prototype = new Person( )
var w = new Web( '赵四' , 20 )  //实例化子类 的时候 没法给父类传参
w.run( ) // this.name undefined   找不到 name
```

```js
// 原型链+构造函数的组合继承方式
function Person(name, age ) {
    this.name = name
    this.age = age
    //构造函数定义
    this.run = function( ){
        alert( this.name + '在运动')
    }
}
//原型链定义   原型链上的属性会被多个实例共享  构造函数不会
Person.prototype.sex = '男'
Person.prototype.work = function( ) {
    alert( this.name + '在工作' )
}
function Web ( name , age  ) {
    Person.call(this,name,age)  //对象冒充继承 可以继承构造函数里面的属性和方法   实例化子类 可以给父类传参
}
Web.prototype = new Person( )
var w = new Web( '赵四' , 20 )  //实例化子类 的时候 没法给父类传参
w.run( ) 
```

### typescript 类

1. typescript 定义类

```js
class Person {
    name : string      // 属性  前面省略了 pubic 关键字
    constructor( n : string ) {   // 构造函数           实例化类的 时候触发的方法
        this.name = n
    }
    run( ) : void {
        alert ( this.name )
    }
}
var p = new Person( '张三' )
p.run( )
```



```js
class Person {
    name : string      // 属性  前面省略了 pubic 关键字
    constructor( name : string ) {   // 构造函数           实例化类的 时候触发的方法
        this.name = name
    }
    getName( ): string{
        return this.name
    }
    setName( name : string ) : void {
        this.name = name
    }
}
var p = new Person( '张三' )
alert( p.getName( ) )   //获取name 张三
p.setName( '李四' )  // 设置name 李四
alert( p.getName( ) )  // 获取name 李四
```



2. TS 中实现继承  extends 和 super

```js
class Person{
    name: string
    constructor ( name: string ){
        this.name = name 
    }
    run( ) : string {
        return `${this.name}在运动`
    }
}
var p = new Person( '王五' )
alert( p.run( ) )    // 王五在运动
```

* 继承

```js
class Person{
    name: string
    constructor ( name: string ){
        this.name = name 
    }
    run( ) : string {
        return `${this.name}在运动`
    }
}
class Web extends Person {
    constructor ( name : string ){
        super ( name )    // 初始化 父类的构造函数
    }
}
var w = new Web( '李四' )
alert ( w.run( ) )  //李四在运动
```

* ts中继承的  父类的方法和子类的一致

```js
        class Person{
            name:string;
            constructor(name:string){
                this.name=name;
            }
            run():string{
                return `${this.name}在运动`
            }
        }
        class Web extends Person{
            constructor(name:string){
                super(name);  /*初始化父类的构造函数*/
            }
            run():string{
                return `${this.name}在运动-子类`
            }
            work(){
                alert(`${this.name}在工作`)
            }
        }
        var w=new Web('李四');
        // alert(w.run());
        w.work();   // 
        alert(w.run());  // 执行子类的 方法   先找本身 在找父类
```

### 类里面的修饰符

1. ts 里面在定义属性的时候定义了三种修饰符`public`(公有)、`protected`(保护类型)、`private`(私有)

   属性如果不加修饰符 默认就是 公有 （public）

* **public** :公有     在当前类里面、 子类 、类外面都可以访问

```js
              class Person{
                    public name:string;  /*公有属性*/
                    constructor(name:string){
                        this.name=name;
                    }
                    run():string{
                        return `${this.name}在运动`
                    }
                }
                class Web extends Person{
                    constructor(name:string){
                        super(name);  /*初始化父类的构造函数*/
                    }
                    run():string{
                        return `${this.name}在运动-子类`
                    }
                    work(){
                        alert(`${this.name}在工作`)
                    }
                }
                var w = new Web('李四');
                w.work();  // 子类里 可以访问 public 属性
```

* 类外部访问公有属性

```js
                  class Person{
                    public name:string;  /*公有属性*/
                    constructor(name:string){
                        this.name=name;
                    }
                    run():string{
                        return `${this.name}在运动`
                    }
                }
                var  p=new Person('哈哈哈');
                alert(p.name);  //   可以访问
```

* **protected**：保护类型  在类里面、子类里面可以访问 ，在类外部没法访问

```js
              class Person{
                    protected name:string;  /*保护类型*/
                    constructor(name:string){
                        this.name=name;
                    }
                    run():string{
                        return `${this.name}在运动`
                    }
                }
                var p=new Person('王五');
                alert(p.run())  // 当前类 里可以访问
                class Web extends Person{
                    constructor(name:string){
                        super(name);  /*初始化父类的构造函数*/
                    }                  
                    work(){
                        alert(`${this.name}在工作`)
                    }
                }
                var w=new Web('李四11');
                w.work();   //  可以在 子类 里访问 保护属性
                alert( w.run());  // 子类 里访问 保护属性
```

* 类外外部没法访问保护类型的属性

```js
                class Person{
                    protected name:string;  /*保护类型*/
                    constructor(name:string){
                        this.name=name;
                    }
                    run():string{
                        return `${this.name}在运动`
                    }
                }
                var  p=new Person('哈哈哈');
                alert(p.name);    //类外部 不可访问 保护类型 书写时回报错
```

* **private** ：私有    在类里面可以访问，子类、类外部都没法访问

 ```js
                class Person{
                    private name:string;  /*私有*/
                    constructor(name:string){
                        this.name=name;
                    }
                    run():string{
                        return `${this.name}在运动`
                    }
                }
                class Web extends Person{
                    constructor(name:string){
                        super(name)
                    }
                    work(){
                        console.log(`${this.name}在工作`)  //报错 无法访问
                    }
                }
 ```

* 内部访问

```js
    class Person
        private name:string;  /*私有*/
        constructor(name:string){
            this.name=name;
        }
        run():string{
            return `${this.name}在运动`
        }
    }
    var p=new Person('哈哈哈');
    alert(p.run());      //内部可以访问
```

### 静态属性

```js
    function Person(){
        this.run1=function(){
        }
    }
    Person.name='哈哈哈';
    Person.run2=function(){    //静态方法
    }
    var p=new Person();  
    Person.run2(); 静态方法的调用
```

* JQ中的属性和方法

```js
        function $(element){
            return new Base(element)
        }
        $.get=function(){            //静态方法
        }
        function Base(element){
            this.element=获取dom节点;
            this.css=function(arr,value){
                this.element.style.arr=value;
            }
        }
        $('#box').css('color','red')  // 实例方法调用
        $.get('url',function(){    //静态方法调用
        })
```

* ts 定义静态方法  `static`关键词

```js
    class Per{
        public name:string;
        public age:number=20;
        //静态属性
        static sex="男";
        constructor(name:string) {
                this.name=name;
        }
        run(){  /*实例方法*/
            alert(`${this.name}在运动`)
        }
        work(){
            alert(`${this.name}在工作`)
        }
        static print(){  /*静态方法  里面没法直接调用类里面的属性*/
            alert('print方法'+Per.sex); //静态方法 可以调用静态属性
        }
    }
    // var p=new Per('张三');
    // p.run();
    Per.print();
    alert(Per.sex);
```



### 抽象类 继承多态

1. **多态:**父类定义一个方法不去实现，让继承它的子类去实现 每一个子类有不同的表现

   多态属于继承

```js
                class Animal {
                    name:string;
                    constructor(name:string) {
                        this.name=name;
                    }
                    eat(){   //具体吃什么  不知道   ，  具体吃什么?继承它的子类去实现 ，每一个子类的表现不一样
                        console.log('吃的方法')
                    }
                }
                class Dog extends Animal{
                    constructor(name:string){
                        super(name)
                    }
                    eat(){               
                        return this.name+'吃粮食'
                    }
                }
                class Cat extends Animal{
                    constructor(name:string){
                        super(name)
                    }
                    eat(){
                        return this.name+'吃老鼠'
                    }
                }
```

2. **抽象类**

   typescript中的抽象类：它是提供其他类继承的基类，不能直接被实例化。

   用`abstract`关键字定义抽象类和抽象方法，抽象类中的抽象方法不包含具体实现并且必须在派生类中实现。

   `abstract`抽象方法只能放在抽象类里面

   抽象类和抽象方法用来定义标准 。  标准：Animal 这个类要求它的子类必须包含eat方法

   标准:

```js
abstract class Animal{                //Animal  抽象类 基类
    public name:string;
    constructor(name:string){
        this.name=name;
    }
    abstract eat():any;  //抽象方法不包含具体实现并且必须在派生类中实现。   
    run(){
        console.log('其他方法可以不实现')
    }
}
// var a=new Animal() /*错误的写法*/
class Dog extends Animal{
    //抽象类的子类必须实现抽象类里面的抽象方法
    constructor(name:any){
        super(name)
    }
    eat(){
        console.log(this.name+'吃粮食')
    }
}
var d=new Dog('小花花');
d.eat();
class Cat extends Animal{
    //抽象类的子类必须实现抽象类里面的抽象方法
    constructor(name:any){
        super(name)
    }
    run(){
    }
    eat(){
        console.log(this.name+'吃老鼠')
    }   
}
var c=new Cat('小花猫');
c.eat();
```



## typeScript中的接口

**接口的作用：**在面向对象的编程中，接口是一种规范的定义，它定义了行为和动作的规范，在程序设计里面，接口起到一种限制和规范的作用。接口定义了某一批类所需要遵守的规范，接口不关心这些类的内部状态数据，也不关心这些类里方法的实现细节，它只规定这批类里必须提供某些方法，提供这些方法的类就可以满足实际需要。 typescrip中的接口类似于java，同时还增加了更灵活的接口类型，包括属性、函数、可索引和类等。

通过 `interface`定义接口

### 属性类接口

* 对json的约束

```js
//ts中定义方法
        function printLabel():void {
            console.log('printLabel');
        }
        printLabel();
```

```js
//ts中定义方法传入参数
        function printLabel(label:string):void {
            console.log('printLabel');
        }
        printLabel('hahah');
```

* ts中自定义方法传入参数,对json进行约束

```js
        function printLabel(labelInfo:{label:string}):void {
            console.log('printLabel');
        }
//参数 需要 传入一个对象  对象里边为字符串
        printLabel('hahah'); //错误写法


        printLabel({name:'张三'});  //错误的写法


        printLabel({label:'张三'});  //正确的写法
```

* 对批量方法传入参数进行约束。

1. **对象类型接口：**行为和动作的规范，对批量方法进行约束

```js
//就是传入对象的约束    属性接口
         interface FullName{
            firstName:string;   //注意;结束
            secondName:string;
        }
        function printName(name:FullName){
            // 必须传入对象  firstName  secondName
            console.log(name.firstName+'--'+name.secondName);
        }
        // printName('1213');  //错误
        var obj={   /*传入的参数必须包含 firstName  secondName*/
            age:20,
            firstName:'张',
            secondName:'三'
        };
        printName(obj)
```

```js
            interface FullName{
                firstName:string;   //注意;结束
                secondName:string;
            }
            function printName(name:FullName){
                // 必须传入对象  firstName  secondName
                console.log(name.firstName+'--'+name.secondName);
            }
            function printInfo(info:FullName){
                // 必须传入对象  firstName  secondName
                console.log(info.firstName+info.secondName);
            }
            var obj={   /*传入的参数必须包含 firstName  secondName*/
                age:20,
                firstName:'张',
                secondName:'三'
            };
            printName(obj);
            printInfo({
                firstName:'李',
                secondName:'四'
            })
```

2. **接口 ：可选属性**

   通过`？`标志属性需不需要传，为可选属性

```js
    interface FullName{
        firstName:string;
        secondName:string;
    }
    function getName(name:FullName){
        console.log(name)
    }
    //参数的顺序可以不一样
    getName({        
        secondName:'secondName',
        firstName:'firstName'
    })
```

```js
    interface FullName{
        firstName:string;
        secondName?:string;
    }
    function getName(name:FullName){
        console.log(name)
    }  
    getName({               
        firstName:'firstName'
    })
```

**例子：**

```js
//原生JS封装ajax
interface Config {
    type:string
    url:string
    data?:string
    dataType:string
}
function ajax(config:Config) {
    var xhr = new XMLHttpRequest()
    xhr.open(config.type,config.url,true)
    xhr.send(config.data)
    xhr.onreadystatechange = function(){
        if (xhr.readyState==4 && xhr.status==200) {
            console.log('success');        
            if (config.dataType=='json') {
                console.log(JSON.parse(xhr.responseText));    
            }else{
                console.log(xhr.responseText);                
            }
        }
    }
}
ajax({
    type:'get',
    data:'name=zhangsan',
    url:'http://a.itying.com/api/productlist',
    dataType:'json'
})
```

### **函数类型接口：**

​	对方法传入的参数 以及返回值进行约束  批量约束

* 加密的函数类型接口

```js
interface encrypt{
    (key:string,value:string):string;
}
var md5:encrypt=function(key:string,value:string):string{
        //模拟操作
        return key+value;
}
console.log(md5('name','zhangsan'));
var sha1:encrypt=function(key:string,value:string):string{
    //模拟操作
    return key+'----'+value;
}
console.log(sha1('name','lisi'));
```

### 可索引接口

**可索引接口：**数组、对象的约束 （不常用）

```JS
 //ts定义数组的方式
            var arr:number[]=[2342,235325]
            var arr1:Array<string>=['111','222']
```

```js
//可索引接口 对数组的约束
interface UserArr {
    [index:number]:string
}
var arr:UserArr=['123','5555']
console.log(arr[0]);
```

```js
//可索引接口 对象约束
interface UserObj{
    [index:string]:string
}
var arr:UserObj = {
    name:'lili'
}
```

### 类类型接口

**类类型接口：**对类的约束 和  抽象类抽象有点相似 

使用 `implements` 关键字实现接口

```js
interface Animal{
    name:string
    eat(str:string):void
}
class Dog implements Animal {
    name:string
    constructor(name:string) {
        this.name = name
    }
    eat(){
        console.log(this.name+'吃肉');
    }
}
var d = new Dog('小黑')
d.eat()
class Cat implements Animal {
    name:string
    constructor(name:string) {
        this.name = name
    }
    eat(food:string){
        console.log(this.name+'吃'+food);        
    }
}
var c = new Cat('花花')
c.eat('老鼠')
```

### 接口扩展

* **接口扩展：**接口可以继承接口

```js
interface Animal {
    eat():void
}
interface Person extends Animal {
    work():void
}
class Web implements Person {
    public name:string
    constructor(name:string) {
        this.name = name
    }
    eat(){                      //接口中 定义的 属性和方法 必须要有
        console.log(this.name+'喜欢吃肉肉');        
    }
    work(){                      //接口中 定义的 属性和方法 必须要有
        console.log(this.name+"爱工作");       
    }
}
var w = new Web('小李')
w.work()
w.eat()
```

* **例子：**类继承+接口继承

```js
interface Animal {
    eat():void
}
interface Person extends Animal {
    work():void
}
class Progrommer {
    public name:string
    constructor(name:string) {
        this.name = name 
    }
    coding(code:string){
        console.log(this.name+code);   
    }
}
class Web extends Progrommer implements Person {
    constructor(name:string) {
        super(name)
    }
    eat(){
        console.log(this.name+'喜欢吃肉肉');        
    }
    work(){
        console.log(this.name+"爱工作");       
    }
}
var w = new Web('小李')
w.work()
w.eat()
w.coding('写代码')
```

## typeScript中的泛型

### 泛型的定义

1. **什么是泛型：**泛型的本质是参数化类型，通俗的将就是所操作的数据类型被指定为一个参数，这种参数类型可以用在类、接口和方法的创建中，分别成为泛型类，泛型接口、泛型方法

2. **为什么使用泛型：**ypeScript 中不建议使用 any 类型，不能保证类型安全，调试时缺乏完整的信息。

   TypeScript可以使用泛型来创建`可重用`的组件。支持当前数据类型，同时也能支持未来的数据类型。扩展灵活。可以在编译时发现你的类型错误，从而保证了类型安全。

3. **泛型：**软件工程中，我们不仅要创建一致的定义良好的API，同时也要考虑可重用性。 组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。

   在像`C#`和`Java`这样的语言中，可以使用泛型来创建可重用的组件，一个组件可以支持多种类型的数据。 这样用户就可以以自己的数据类型来使用组件。

   **通俗理解：**泛型就是解决 类 接口 方法的复用性、以及对不特定数据类型的支持(类型校验)

### 泛型函数

```js
//只能返回 string 类型
function getData(value:string):string {
    return value
}
```

* 定义泛型   `< T >`  表示泛型，具体什么类型是调用这个方法决定的

```js
function getData<T>(value:T):T {
    return value 
}
getData<number>(123)
getData<number>('123')   //错误
getData<string>('1222')
```

### 泛型类

* **泛型类：**比如有个最小堆算法，需要同时支持返回数字和字符串 a - z两种类型。 通过类的泛型来实现

```js
           //普通写法
	class MinClass{
                public list:number[]=[];
                add(num:number){
                    this.list.push(num)
                }
                min():number{
                    var minNum=this.list[0];
                    for(var i=0;i<this.list.length;i++){
                        if(minNum>this.list[i]){
                            minNum=this.list[i];
                        }
                    }
                    return minNum;
                }
            }
            var m=new MinClass();
            m.add(3);
            m.add(22);
            m.add(23);
            m.add(6);
            m.add(7);
            alert(m.min());
```

```js
//类的泛型
class MinClas<T>{
    public list:T[]=[];
    add(value:T):void{
        this.list.push(value);
    }
    min():T{        
        var minNum=this.list[0];
        for(var i=0;i<this.list.length;i++){
            if(minNum>this.list[i]){
                minNum=this.list[i];
            }
        }
        return minNum;
    }
}
var m1=new MinClas<number>();   /*实例化类 并且制定了类的T代表的类型是number*/
m1.add(11);
m1.add(3);
m1.add(2);
alert(m1.min())
var m2=new MinClas<string>();   /*实例化类 并且制定了类的T代表的类型是string*/
m2.add('c');
m2.add('a');
m2.add('v');
alert(m2.min())
```

使用泛型的好处：不仅有类型校验，还可以规定传入类型

* **把类作为参数的泛型类**

  定义一个User的类这个类的作用就是映射数据库字段 

  然后定义一个 MysqlDb的类这个类用于操作数据库  

  然后把User类作为参数传入到MysqlDb中

```js
把类作为参数来约束数据传入的数据类型
class User {
    public username:string|undefined
    public password:string|undefined
}
class MysqlDb {
    add(user:User):boolean{
        console.log(user);
        return true
    }
}
var u = new User()
u.username = '张三'
u.password = '123456'
var Db = new MysqlDb()
Db.add(u)
```

```js
class ArticleCate {
    public title:string|undefined
    public desc:string|undefined
    public status:number|undefined
}
class MysqlDb {
    add(info:ArticleCate):boolean{
        console.log(info);        
        console.log(info.title);        
        return true
    }
}
var a = new ArticleCate()
a.title = "国内"
a.desc = "国内新闻"
a.status = 1
var Db = new MysqlDb()
Db.add(a)
```

* **泛类：**泛型可以帮助我们避免重复的代码以及对不特定数据类型的支持(类型校验)，把类当做参数的泛型类

```js
//操作泛型类的数据库
class MysqlDb<T> {
    add(info:T):boolean{
        console.log(info);        
        return true
    }
    updata(info:T,id:number):boolean{
        console.log(info);
        console.log(id);       
        return true
    }
}
//想给User表增加数据
// 1 定义一个User类 和数据库进行映射
class User {
    username:string|undefined
    password:string|undefined
}
var u = new User()
u.username = "张三"
u.password = "123456"

// 2 定义一个文章分类的类 和数据库进行映射
class ArticleCate {
    title:string|undefined
    desc:string|undefined
    status:number|undefined
    constructor(params:{
        title:string|undefined,
        desc:string|undefined,
        status?:number|undefined
    }){
        this.title = params.title
        this.desc = params.desc
        this.status = params.status
    }
}
//增加操作
var a = new ArticleCate({
    title:'分类',
    desc:'1111'
})
//类当参数的泛型类
var Db = new MysqlDb<ArticleCate>()
Db.add(a)
var b = new ArticleCate({
    title:'企业',
    desc:'123'
})
b.status=0
var CC = new MysqlDb<ArticleCate>()
CC.updata(b,12)
```



### 泛型接口

* 定义一个函数接口

```js
        interface ConfigFn{
            (value1:string,value2:string):string;
        }
        var setData:ConfigFn=function(value1:string,value2:string):string{
            return value1+value2;
        }
        setData('name','张三');
```

* 泛型接口 方法1

```js
        interface ConfigFn{
            <T>(value:T):T;
        }
        var getData:ConfigFn=function<T>(value:T):T{
            return value;
        }
         getData<string>('张三');
         getData<string>(1243);  //错误
```

* 泛型接口 方法2

```js
        interface ConfigFn<T>{
            (value:T):T;
        }
        function getData<T>(value:T):T{
            return value;
        }    
        var myGetData:ConfigFn<string>=getData;     
        myGetData('20');  /*正确*/
        myGetData(20)  //错误
```



