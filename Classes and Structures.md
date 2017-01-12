####Classes and Structures

Class 和 Structure 是一种构建程序的通用灵活的"砖头"(我们就是搬砖的). 我们可以使用几乎一样的语法来给我们的class 和 structure来定义properties(比如常量和变量)和methods(比如function)很方法来扩展它们的功能.

* Swift 类的interface和implementation在同一个文件中,这样面向外部代码的 external interface就会自动生成.

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
  * Type casting(格式转换) enables you to check and interpret the type of a class instance at runtime.
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
来指定structure中的初始化值.
```Swift
let vag = Resolution(width: 640, height: 480)
```
**Structures and Enumerations Are Value Types**

* A value type is a type whose value is copied when it is assigned to avriable or constant, or when it is passed to a function.

* All the basic types in Swift- integers, floating-point numbers, Booleans, strings, arrays, and dicitonaries- are value types, and are implemented as structures behind the scenes.
* All Structures and enumerations are value types in Swift. This means that any structure and enumeration instances you create-- and any value types they have as properties -- are **always** copied when they are passed around in your code.

**Classes Are Reference Types**

Unlike value types, `reference type` are not copied when they assigned to a variable or constant, or when they are passed to a function. Rather than a copy, a reference to the same existing instance is used instead.

**Identity Operators**

* Identical to ( === )
* Not identical t0 ( !== )

**NOTE:**
* "Identical to" means that two constance or variables of class type refer to exactly the same class instance.
* "Equal to" means that two instances are considered "equal" or "equivalent" in value, for some appropriate meaning of "equal",  as defined by the type's designer.

**Choosing Between Classes and Structures**

consider creating a structure when one or more of these conditions apply:
* The structure's primary purpose is encapsuate a few relatively simple data values.
* It is reasonable to expect that the encapsulated values will be copied rather than referenced when you assign or pass around an instance of that structure.
* Any properties stored by the structure are themselves value types, which would also be expected to be copied rather than referenced.
* The structure does not need to inherit properties or behavior from another exiting type.

**Assignment and Copy Behavior for Strings, Arrays, and Dictionaries**

* String, Array, Dictionary are implemented as structures. 


























  