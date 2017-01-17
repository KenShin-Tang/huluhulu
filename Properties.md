####Properties

**Stored Properties** 用来存储实例的常量/变量值(class, structure 才有); **Computed Properties** 计算出值(而不是存储, class structure, Enumeration 都可以有).

* 我们可以定义 property observer 来监测 property 值的变化(用来响应值的变化), 它可以被添加到自定义的 stored properties或者继承自父类的 properties.

**Stored Properties

* 简答来说, stored property 就是 class/structure实例中存储的一个常量或者变量值.
* 属性在定义时可以预置一个默认值, 也可以在初始化的时候设置/修改其值(constant除外).

**Stored Properties of Constant Structure Instances

我们不能修改常量结构体类型的实例,即使此结构体中我们定义有var也不行,因为 constant的结构体本身是不能修改的.

**Lazy Stored Properties

A lazy stored property is a property whose initial value is not calculated until the first time it is used. You indicate a lazy stored property by writing the `lazy` modifier before its declaration.

*NOTE: `lazy` 只能用于变量, 因为它的初值有可能在实例初始化后也不一定会有. 而常量property在初始化完成之前必须有初始值.*

Lazy properties are useful when the initial value for a property is dependent on outside factors whose value are not known until after an intance's initialization is complete. Lazy properties are also useful when the initial value for a property requires complex or computationally expensive setup that should not be performed unless or until it is needed.

*NOTE: 多线程下` lazy` 修饰的 property 默认有可能被初始化多次(即不安全)*

**Stored Properties and Instance Variables**

在 OC 中, 有两种方式来存储  值和引用 作为类实例的一部分.一个是 property, 一个是实例变量(用来备份存储在 property 中的值). 而 Swift 则将两者融合成一个 property 声明. Swift 的 property 没有对应的 instance variable, 且property 的backing store(值备份) is not accessed directly. 这就避免了像 OC 一样,有时用 property 访问有时用 instance variable 访问的困惑.

**Computed Properties**
In addition to stored properties, classes, structures, and enumerations can define computed properties, which *do not actually store a value. Instead, they provide a getter and and an optional setter to retrieve and set other properties and vlaue inderectly*.

**Shorthand Setter Declaration**

computed property的 setter 默认以" newValue" 为新值的 name, 当然也可以选择性地指定.

**Read-Only Computed Properties**
    A computed property with a getter but no setter is known as a `read-only computed property`.
    
*NOTE: computed properties 必定是变量,即以 `var`修饰, 因为它们的值不固定, 是计算出来的.*

* 我们对于只读属性甚至可以省略`get`关键字以及对应的花括号. 

**Property Observers**

Property observers观察并响应其 property 值的变化即便是前后 set 的是相等的值.

You can add property observers to any **stored properties** you define, except for lazy stored properties.
我们可以选择性地定义一下两个中的任意一个或同时都定义:
* `willSet` is called just before the value is strored.默认的新值名字为 newValue.
* `didSet` is called immediately after the new value is stored. 默认老值的 name 是 oldValue.

**Global and Local Variables**
Global constants and variables are always computed lazily, in a similar manner to Lazy Stored Properties. Unlike lazy stored properties, global constants and variables do not need to be marked with the lazy modifier. Local constants and variables are never computed lazily.

**Type Properties**
实例的属性从属于某个特定类型的实例,每次创建一个这个类型的实例的时候, 这个实例就会有一系列的属性值, 从而与 其他同类型的实例区分开来.

我们也可以定义只从属与类型本身的一类属性, 它不从属于这种类型实例. 这些properties只会有一份copy, 无论这种类型的实例创建多少个. 这类属性就叫做`Type Property`.

`Type Properties` 在定义特定类型的某些属性只有一个通用的属性值的时候很有用,比如常量属性(类似的在C中的static constant)或者 一个对于所有实例来说是全局变量的变量属性(比如C中的static variable).

* Type property 必须有默认值.
* 使用 `static`关键字标注.

































