####Classes and Structures

Class 和 Structure 是一种构建程序的通用灵活的"砖头"(没错,我们就是搬砖的). 我们可以使用几乎一样的语法来给我们的class 和 structure来定义properties(比如常量和变量)和methods(比如function)很方法来扩展它们的功能.

* Swift 类的interface和implementation在同一个文件中,这样面向外部代码的 external interface就直接生成了,不必再像 C/C++ 分开写.

Class 与 Structure的比较:
1. 相同点:

  * 使用properties存储值
  * 使用methods实现功能
  * 使用"subscripts"用于访问其或其内部的值 array[index]   dictionary[key]
  * 使用构造器(或者称initializer)初始化其值
  * 都可以拓展(即使用extension)
  * Confirm to protocols to provide standard functionality of a certain kind

2.Classes 具备但Structures不具备的特点:
  * 继承.
  * Type casting(类型转换) enables you to check and interpret the type of a class instance at runtime.
  * 析构.
  * 引用计数.

Structure 通常是"值copy"的方式在代码中传递, 而不使用引用计数.

**Definition Syntax**

```Swift
class SomeClass {
  //class definition goes here
}

struct SomeStructure {
  //structure definition goes here
}
```

我们使用他们的构造器(initailizer)来创建一个instance.比如:
```Swift
let someResolution = Resolution()
let someVideoMode = VideoMode()
```
* 使用点语法来访问properties. 也可以使用连续的点语法来"钻取"数据.如
```Swfit
someVideoMode.resolution
someVideoMode.resolution.width
```
**NOTE:** Unlike Objective-C, Swift enables you to set sub-properties of a structure property directly. In the last example above, the width property of the resolution property of someVideoMode is set directly, without your needing to set the entire resolution property to a new value.

我们也可以使用 Memberwise Initializers for **Structure Types**
来指定structure中的初始化值相应的参数名即是 properties 的 name.
```Swift
let vag = Resolution(width: 640, height: 480)
```
**Structures 和 Enumeration 都是值类型(Value Type)**

* 值类型(Value type)即赋值给变量/常量或者传递给函数作为参数时, 都是一份"原值"的copy.

* Swift 中所有的基本类型- integers, floating-point numbers, Booleans, strings, arrays, and dicitonaries- 都是值类型且背后都是以 structure 来实现的.
*  Swift 中所有的Structures 和 Enumeration 都是值类型. 这就意味着任何 structure 和 enumeration 的实例或者他们拥有的值类型的属性 -- 在传递时通常都是**copy** 的.

**Classes是引用类型(Reference Types)**

与值类型不同, 引用类型(`reference type`) 在传递过程中不会被 copy, 而是对同一个实例的引用.

**Identity Operators**

* Identical to ( === )
* Not identical t0 ( !== )

**NOTE:**
* "Identical to"(===)用来说明两个常量或者变量(类型为class) 引用了同一个类实例.
* "Equal to" 是说两个实例是等值的.

#### Pointers



#### **Choosing Between Classes and Structures**

两者如何选择呢, 潜规则:
* The structure's primary purpose is encapsuate a few relatively simple data values.
* It is reasonable to expect that the encapsulated values will be copied rather than referenced when you assign or pass around an instance of that structure.
*  structure 中的 properties 自身也要是值类型, 所以class 与 structure 最好不要混用.
* 没有继承(或者说不需要继承).

在大多数与图形相关的场景中, 比如坐标, 点位等使用 structure 挺好. 其他场景则最好使用 class, 其实大多数的自定义数据结构还是使用 class 而不是 structure.

**Assignment and Copy Behavior for Strings, Arrays, and Dictionaries**

*  在 Swift 中String, Array, Dictionary 是以 structure 来实现的(即值类型), 而 Foundation 中的NSArray, NSString, NSDictionary 则是用 class来实现的(即引用类型). 所以要分清在什么框架下.


























  