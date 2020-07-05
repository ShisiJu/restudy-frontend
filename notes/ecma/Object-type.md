#  JS Object Type

JS中的对象(Object)是比较复杂的. 在ECMA中的定义还是比较清晰的; 
这里翻译一下, 分享给大家.

因为本节内容有许多的表格, 我有翻译, 但也给了大家链接, 原版的可以自己查阅.

原文地址: [ECMAScript Object Type](https://www.ecma-international.org/ecma-262/11.0/index.html#sec-object-type)

## The Object Type

对象(Object) 是属性的逻辑上的集合(collection). 
每个一个属性(property) 不是 `数据属性(data property)` 就是 `访问器属性 (accessor property)`
数据属性的key值与ECMAScript语言的值和一系列布尔类型(Boolean)的特征(attributes)相关联. (后面有解释)

访问器属性的key值与一个或两个访问器函数以及一系列布尔类型(Boolean)的特征(attributes)相关联.
访问器函数被用于存储和查询相关联的属性的ECMAScript语言值.

属性(Properties) 通过 key 识别.

一个属性的key 有两种类型

* String (包括空字符串)
* Symbol

属性名是一个属性键，它是一个字符串值。

> ECMAScript语言值 就是 JS 中的数据值, 例如 null, undefined , object 等等

一个整型的索引(index)是一个 String-valued 的属性key, 它是规范的数字字符串, 并且它的数字值范围是 +0(正数0) 和 2^53 -1 之间.

一个数组的索引是一个整数索引, 它的范围是在 +0 到 2^32 -1 之间.

如果, 使用数字作为key, 会默认转成字符串. 但是, 在数据超过 2^53 -1 时, 会使用科学计数法.

``` js
var q = {
    8390812903912839012903891839018390129381938912083918390131830912839: 'hello'
}
// undefined
q['8390812903912839012903891839018390129381938912083918390131830912839']
// hello
q['8.390812903912838e+66']
```

属性的key用于存取属性和它们的值. 
这又两种不同的存取属性. get 和 set, 对应着获取和分配.

属性通过get 和 set来存取

* 这个对象自己拥有的属性
* 通过继承关系来指向到另一个相关联的对象的属性

`继承的属性(Inherited properties)` 可以是它自己的属性, 也又可能是它从另外一个相关联的对象中继承而来的.

对象的每个属性都必须具有一个键值，该键值与该对象的其他属性的键值不同。

所有对象都是属性的逻辑集合. 有多种形式的对象，它们在访问和操作属性时的语义上各不相同

## Property Attributes

特征用于定义和解释对象属性的状态(state). 



### Attributes of a Data Property

一个数据属性和它关联的的值以及特征在下面的表格中


| 属性名           | 值域             | 描述                                                                                          |
| ---------------- | ---------------- | --------------------------------------------------------------------------------------------- |
| [[Value]]        | 任意ECMA语言的值 | 通过get 来获取到的值                                                                          |
| [[Writable]]     | Boolean          | 如果是false, 尝试改变 [[Value]]的操作都将失败                                                 |
| [[Enumerable]]   | Boolean          | 如果是true, 这个属性可以被for-in 枚举. 否则, 这个属性是 不可枚举的                            |
| [[Configurable]] | Boolean          | 如果设置位false, 尝试删除, 改变这个属性的特征的操作都将失败.(无论是[[Value]]还是[[Writable]]) |

### Attributes of an Accessor Property

访问器属性, 相关的特征如下表

[Table 4: Attributes of an Accessor Property](https://www.ecma-international.org/ecma-262/11.0/index.html#table-3)


| 属性名           | 值域                  | 描述                                                                                                                                                                                                      |
| ---------------- | --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [[Get]]          | Object 或者 Undefined | 如果是对象,必须是函数对象. 这个函数的[[Call]]内部方法是一个被空参数列表调用的, 用于查询这个属性值.每次获取属性时,执行它.                                                                                  |
| [[Set]]          | Object 或者 Undefined | 如果是对象,必须是函数对象, 这个函数的[[Call]]内部方法是一个带有一个要赋值的值参数的函数.在每次给属性赋值时执行.属性的[[Set]]内部方法的效果可能(但不是必需的)影响后续调用该属性的[[Get]]内部方法返回的值。 |
| [[Enumerable]]   | Boolean               | 如果是true, 这个属性可以被for-in 枚举. 否则, 这个属性是 不可枚举的                                                                                                                                        |
| [[Configurable]] | Boolean               | 如果设置位false, 尝试删除, 改变这个属性的特征的操作都将失败.(无论是[[Value]]还是[[Writable]])                                                                                                             |


### Default Attribute Values

如果初始化的特征的值没有被显式指定, 默认值如下表


[Table 5: Default Attribute Values](https://www.ecma-international.org/ecma-262/11.0/index.html#table-default-attribute-values)

| Attribute Name   | Default Value |
| ---------------- | ------------- |
| [[Value]]        | undefined     |
| [[Get]]          | undefined     |
| [[Set]]          | undefined     |
| [[Writable]]     | false         |
| [[Enumerable]]   | false         |
| [[Configurable]] | false         |


### 结合MND 学习

前面说的有些模糊, 我们结合通过MDN, 一起来学习一下 属性.

[defineProperty](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

[getOwnPropertyDescriptor](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/getOwnPropertyDescriptor)


MDN 中讲解的很好, 我就不重复写例子了. 


## Object Internal Methods and Internal Slots

在ECMAScript中, 对象的实际语义是通过`内部方法(internal methods)`的算法所指定的.

在ECMAScript引擎中的每一个对象都和一系列内部方法相关.这些内部方法定义了对象的`运行时行为(runtime behaviour)`.
这些内部方法不是ECMAScript语言的一部分. 它们被文档所定义存粹是为了说明的目的.

然而, ECMAScript实现中的每个对象都必须按照与其关联的内部方法指定的行为.

> 说人话, 就是JS中的对象的行为, 其实是由一些内部方法来控制的. 但是, 这些方法不属于JS层面, 而是属于更底层的实现. 

内部方法的名称是多态的(polymorphic). 这就意味着当一个常见的内部方法被调用时, 不同的对象值可能执行不同的算法.
调用内部方法的实际对象是调用的“目标”。

在运行时, 如果一个算法的实现尝试使用一个对象的不支持的内部方法, 会抛出 `TypeError` 的异常.

`内部插槽(Internal slots)`对应着`内部状态(internal state)`, 它与对象相关联, 并且被多种ECMAScript规范算法所引用.

内部插槽不是对象的属性, 它们不会被继承. 
取决于具体的内部插槽规范, 许多状态可能包含多个ECMAScript语言类型或者ECMAScript规范类型.

除非由特别的说明, 内部插槽是在创建对象的过程中分配的，不能动态地添加到对象中.

除非由特别的说明,内部插槽的初始值是undefined. 

说明中创建对象的多种算法有内部插槽.然而, ECMAScript语言没有提供直接与一个对象内部插槽交互的方式.


> ECMAScript规范类型是指 Reference, List, Completion, Property Descriptor, Lexical Environment, Environment Record, Abstract Closure, and Data Block.  它们是用于描述语义  `元值(meta-value)`
> 这个之后可能给大家翻译一下.


内部方法和内部插槽在本说明文档中通过两个方括号 `[[]]` 来特指.

[表6 ](http://www.ecma-international.org/ecma-262/#table-5)总结了本规范使用的基本内部方法，这些方法适用于ECMAScript代码创建或操作的所有对象。
每个对象都必须有用于所有基本内部方法的算法。但是，并非所有对象都对这些方法使用相同的算法。

这个表是一个说明意义的表, 写了一些常用的内部方法和内部插槽.

`普通的对象(ordinary object)`是需要满足下面的条件的

- 所有在[表6 ](http://www.ecma-international.org/ecma-262/#table-5) 定义的方法, 和[普通对象的内部方法和内部插槽](http://www.ecma-international.org/ecma-262/#sec-ordinary-object-internal-methods-and-internal-slots)
- 如果对象有 [[Call]] 的内部方法, 需要有[对应的实现](http://www.ecma-international.org/ecma-262/#sec-ecmascript-function-objects-call-thisargument-argumentslist)
- 如果对象有 [[Construct]] 的内部方法,需要有[对应的实现](http://www.ecma-international.org/ecma-262/#sec-ecmascript-function-objects-construct-argumentslist-newtarget)


## Ordinary Object Internal Methods and Internal Slots

所有的普通对象有一个内部插槽 `[[Prototype]]`. 这个内部插槽的只可以是 null 或者 一个对象.
它可以被用于继承.

- 数据属性的 [[Prototype]]对象可以被继承(也是对子对象可见的), 可以读, 但是不能修改.
- 访问器属性可能继承get和set.

每一个普通对象都有一个布尔类型值的内部插槽 [[Extensible]] . 它被用于实现可拓展相关的内部方法不变量.
换句话说, 一旦一个对象的[[Extensible]]被设置位false, 它就不再可能给这个对象加入属性, 来修改这个对象的[[Prototype]], 
除非改变这个对象[[Extensible]]为true.

原文中有许多内部方法的定义;
有兴趣可以看看.

[sec-ordinary-object-internal-methods-and-internal-slots](http://www.ecma-international.org/ecma-262/#sec-ordinary-object-internal-methods-and-internal-slots-getprototypeof)


关于对象还有, 外来对象(exotic object), 固有对象(Intrinsic Objects)等等.
精力有限, 就没有翻译.

感兴趣可以去ECMA的官网看看.

