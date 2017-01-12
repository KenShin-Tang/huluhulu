####Properties

**Stored Properties** store constant and variable values as part of an instance, whereas **Computed Properties** calculate(rather than store) a value. **Computed Properties** are provided by classes, structures, and enumerations. **Stored properties** are provided onlly by classes and structures.

**Stored Properties

* 属性在定义时可以预置一个默认值, 也可以在初始化的时候设置/修改其值(constant除外).

**Stored Properties of Constant Structure Instances

我们不能修改常量结构体类型的实例,即使此结构体中我们定义有var也不行,因为 constant的结构体本身是不能修改的.

**Lazy Stored Properties

A lazy stored property is a property whose initial value is not calculated until the first time it is used. You indicate a lazy stored property by writing the `lazy` modifier before its declaration.
*NOTE: You must always declare a lazy property as a variable(with the var keyword), because its initial value might not be retrieved until after intance initialization completes. Constant propertise must always have a value before initializetion completes, and therefore cannot be declared as lazy.*

Lazy properties are useful when the initial value for a property is dependent on outside factors whose value are not known until after an intance's initialization is complete. Lazy properties are also useful when the initial value for a property requires complex or computationally expensive setup that should not be performed unless or until it is needed.
*NOTE: If a property marked with the `lazy` modifier is accessed by multiple threads simultaneously and the property has not yet benn initialized, there is no guarantee that the property will be initialized only once.*

**Stored Properties and Instance Variables**

**Computed Properties**
In addition to stored properties, classes, structures, and enumerations can define computed properties, which *do not actually store a value. Instead, they provide a getter and and an optional setter to retrieve and set other properties and vlaue inderectly*.

**Shorthand Setter Declaration**
If a computed property's setter does not define a name for the new value to be set, a default name of `newValue` is used.

**Read-Only Computed Properties**
    A computed property with a getter but no setter is known as a `read-only computed property`. *NOTE: You must declare computed properties - including read-only computed properties - as variable properties with the `var` keyword, because their value is not fixed. The `let` keyword is only used for constant properties, to indicate that their values cannot be changed noce they are set as part of instance initialization.*

我们对于只读属性甚至可以省略`get`关键字. 

**Property Observers**
Property observers observe and respond to changes in a property's value. Property observers are called every time a property's value is set, even if the new value is the same the property's current value.

You can add property observers to any stored properties you define, except for lazy stored properties.
我们可以选择性地定义一下两个中的任意一个或同时都定义:
* `willSet` is called just before the value is strored.
* `didSet` is called immediately after the new value is stored.

**Global and Local Variables**
Global constants and variables are always computed lazily, in a similar manner to Lazy Stored Properties. Unlike lazy stored properties, global constants and variables do not need to be marked with the lazy modifier. Local constants and variables are never computed lazily.

**Type Properties**
实例的属性从属于某个特定类型的实例,每次创建一个这个类型的实例的时候, 这个实例就会有一系列的属性值, 从而与 其他同类型的实例区分开来.

我们也可以定义只从属与类型本身的一类属性, 它不从属于这种类型实例. 这些properties只会有一份copy, 无论这种类型的实例创建多少个. 这类属性就叫做`Type Property`.

`Type Properties` 在定义特定类型的某些属性只有一个通用的属性值的时候很有用,比如常量属性(类似的在C中的static constant)或者 一个对于所有实例来说是全局变量的变量属性(比如C中的static variable).

* You must always give stored type properties a default value. This is because the type itself dose not have an initializer that can assign a value to a stored type property at initialization time.

































