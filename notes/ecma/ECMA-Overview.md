# ECMAScript Overview  JS综述 

原文地址 [www.ecma-international.org](https://www.ecma-international.org/ecma-262/11.0/index.html#sec-overview)

ECMAScript 前端的同学应该比较熟悉, 是制定JS规范的 Specification. 下文中的 ECMAScript 可以当作JS.
今天, 简单读了一下 Overview 一节, 有一些收获, 这里翻译并加上了一定自己的理解(有增减), 分享给大家.

之后, 想着翻译一下 `6.1.7 The Object Type` (如果有时间, 且想的起来的话...)

## Overview

这一节包含了 `ECMAScript` 的非标准的综述.

ECMAScript 是一个面向对象的编程语言. 它在宿主环境下, 执行计算和操作可计算的对象.
这里定义的ECMAScript, 并不打算在计算上完全靠自己. (有一部分依赖于宿主环境, 例如浏览器,node)
在specification中没有规定 `外部数据的输入` 或者 `计算结果的输出`. 
相对应的, ECMAScript 程序的计算环境不仅提供本规范中描述的这些对象和其它的设施, 也还提供特定环境的特定对象.
除了指出他们可能提供某些属性，可以访问和某些函数，可以调用从ECMAScript程序, 这些描述和行为超出了这篇specification的范围之外.

ECMAScript 原来被设计为用于脚本语言, 但是现在已经变成了有广泛用途的编程语言.
一个脚本语言是用于在一个现有的系统中进行操作,自定义和自动化设备的编程语言.
在这样的系统中，有用的功能已经通过用户接口可用，而脚本语言是一种用于向程序控制暴露该功能的机制.
通过这种方式, 现有的系统提供一个对象和设施的`宿主(host)环境` , 它完善了脚本语言的能力. 

ECMAScript 原本被设计为 Web 脚本语言, 提供一种机制来可以使web页面更为灵活和在 `Web-based` `client-server`结构中执行一部分计算.
ECMAScript 现在被用于在多样的宿主环境中提供核心的脚本能力. 
因此, 在文档中指定的核心语言与特殊的宿主环境无关.

### Web Scripting

一个web浏览器提供了一个 ECMAScript 用于客户端计算的宿主环境, 包括用于展示窗口的对象, 菜单, 弹框, 锚点, 框架, 历史, cookies 等等.
进一步说, 这个**宿主环境提供了一个手段来把脚本代码附加给事件**. 例如焦点的改变, 页面和图片的加载,出错,取消,表单的提交,鼠标的行为.
脚本代码出现在HTML中, 展示的页面是用户界面元素,固定和计算的文本图片的结合.
脚本代码是对用户交互是由响应的, 并且不需要一个主程序.

一个web服务器提供了不同的宿主环境用于服务端的计算, 包括表示请求的对象, 客户端和文件.
这些机制锁住和分享对象. 
通过使用一起使用浏览器端和服务端的脚本, 当给web-base的应用提供一个自定义的用户界面, 
在客户端和服务器之间分发计算结果是有可能的.

每一个支持ECMAScript的web浏览器和服务器提供自己的宿主环境, 使ECMAScript的执行环境变得完整.

### ECMAScript Overview

下面是一个ECMAScript非正式的综述, 它并非标准论文的一部分.

ECMAScript 是面向对象的. 基础的语言和宿主的设备通过对象来提供. 并且 ECMAScript程序是一个通信对象的集群.
在 ECMAScript, 一个对象是0或者多个`属性(properties)`的`集合(collection)`, 每个属性通过`特征(attributes)`来决定每个属性如何使用.

例如, 当一个属性的 `Writable` 特征被设置为 false, 那么任务尝试执行代码来给这个属性分配值的操作都会失败.
属性是拥有其它对象, 原始类型值, 或者 函数的容器 (container). 

原始类型值(primitive value) 是下面集中内置的类型

- Undefined
- Null
- Boolean
- Number
- BigInt
- String
- Symbol

对象是内置类型 `Object` 的一员, 函数(function)是可以调用的对象.
通过属性与对象关联的函数称为方法


ECMAScript定义了一个内置对象集合, 它完善了ECMAScript实体的定义. 这些内置对象包括
下面这些对象对于语言 

- `全局对象 (global object)`
- `运行时语义(runtime semantics)` 的基础, 包括Object, Function, Boolean, Symbol, 和一些 Error 对象
- 用于操作和展示数学相关的对象:  Math, Number, and Date;
- 文本处理对象: String and RegExp
- `有索引的集合 (indexed collections)`:  Array 和 9种不同类型的 Array,  其元素均具有特定的数值数据表示
- `keyed collections 键值对对象` 有 Map , Set 等;
- 结构化对象: JSON 对象, ArrayBuffer, SharedArrayBuffer, 和 DataView; 
- 支持控制抽象化(control abstractions) 有 生成器函数 (generator functions) 和 Promise 对象
- 反射的对象: Proxy 和 Reflect.


ECMAScript 也定义了一系列的 `内置操作符(built-in operators)`. 它们包括: 

- 各种的 一元操作符 unary operation
- 乘法运算符 multiplicative operators
- 加法运算符 additive operators
- 按位移位运算符 bitwise shift operators
- 相等运算符 equality operators
- 二进制按位运算符 binary bitwise operators
- 二进制逻辑运算符 binary logical operators
- 赋值运算符 assignment operators
- 逗号运算符 comma operator 

大型的 ECMAScript 程序通过 `modules` 可以被一个程序被分为多个语句和声明的序列.
每一个模块都显式地确定了声明(declarations). 这些声明说明了模块中引入其它模块的内容, 和哪些内容可以被其它模块引入.

ECMAScript 语法故意地模仿了Java的语法. ECMAScript语法很宽松，可以作为一种易于使用的脚本语言使用.
例如, 一个变量不需要声明它的类型，类型也不需要与属性关联，定义的函数也不需要在调用它们之前以文本形式显示它们的声明。

### Objects

尽管 ECMAScript 有着 class的定义方式, ECMAScript 对象并不是 class-based (基于类)的, 它不像C++ 或者 Java.
相反, 对象可能被多重方式创建

- 字面量 `{}`
- 构造器 (constructor)

构造器, 它创建了对象, 之后执行代码. 通过赋初始值始来初始化所有或者一部分属性(properties).

构造器是一个函数, 它有一个属性 `prototype` 用于实现 `基于原型 (prototype-based)` 的继承和可分享的属性.
对象可以通过构造器或者 new 表达式来创建.
例如 `new Date(2009, 11) ` 创建了一个新的 Date对象.

不通过 new 表达式来调用一个构造器的结果取决于这个构造器.
例如直接 ` Date() ` 就会返回一个表示当前日期的字符串, 而非对象.

构造函数创建的每个对象都有一个 `隐式引用 implicit reference` (称为对象的原型)，该引用指向构造函数的 `prototype` 属性的值。
此外，原型可以具有对其原型的非空隐式引用，等等;

这被称为 `原型链`.

当引用对象中的属性时，该引用是对原型链中包含该名称属性的第一个对象中的同名属性的引用。换句话说,
首先，对直接提到的客体进行这种性质的审查;如果该对象包含命名的属性，则该属性就是引用所引用的属性;如果该对象不包含命名属性，接下来将检查该对象的原型;等等。


上面这段话, 看起来实在是晦涩.
举个例子吧

```js
class Car {
  name(){
    console.log('name')
  }
}

let benz = new Car()
benz.name()
benz.toString()
benz.hello()
```

代码中, Car 是一个 `类` (其实是一个函数, 只是JS为了模拟类, 而特意提供的写法)
`benz.name()` 会去调用 `Car.prototype` 中定义的 `name` 方法.

`benz.toString()` 会先去找 `Car.prototype` 中定义的 `toString()` 方法, 
没有找到, 那就继续向 `Car.prototype`的`prototype` 中去找. 最终在Object的prototype中找打了.就执行它.

`benz.hello()` 会重复上面的步骤, 但是找到Object,发现还是找不到. 那么就会报错 `benz.hello is not a function`

------

在一个 基于类的面向对象语言(例如Java).
一般来说, 状态(state) 是由实例来携带的. 方法(method) 是由class来携带的.
并且, 继承的只有`结构和行为(structure and behaviour)`

但是, 在ECMAScript 状态和方法都是由对象携带的. 同时, 结构,行为和状态都是可以继承的.

所有不直接包含其原型包含的特定属性的对象,共享该属性及其值。

> 原文: All objects that do not directly contain a particular property that their prototype contains share that property and its value. 

不像大多数基于类的语言, ECMAScript中属性可以动态地添加到对象中.也就是说，构造函数不需要为所构造对象的所有或任何属性命名或赋值.

尽管ECMAScript对象本质上不是基于类的，但是基于构造函数、原型对象和方法的公共模式来定义类抽象通常很方便。
ECMAScript内置对象本身遵循这样一个类模式。从ECMAScript 2015开始，ECMAScript语言包括了语法类定义，允许程序员简明地定义符合内置对象使用的相同类抽象模式的对象。

```js
class MyArr extends Array {

}
```

例如, 我们可以对一些内置对象进行拓展.
