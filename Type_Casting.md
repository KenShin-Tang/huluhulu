####Type Casting

* `Type casting` 用来检测实例的类型或者类型转换. 

* Swift 中Type casting 使用`is`(检测类型, 返回值为 true 或 false) 和`as`(转换类型) 操作符.

> NOTE: Casting实际并不会修改/改变实例的值. 在此背后实例维持不变,只是将其看做目标 type 的实例来对待/访问. 

### Downcasting

两种方式`as?` 或者`as!`:

* `as?`在不确定 downcast 是否能成功的情况下使用,将返回一个 optional,即若失败,返回 nil;
* `as!`在确定 downacast 总是成功时使用(强制解包). 如果失败, 则触发 runtime error.


**Type Casting for Any and AnyObject**

Swift內建两种特殊类型别名用于指代非特定类型(即通用类型):
* `AnyObject` 代表一个类(class)的实例, 即对象.
* `Any` 可以代表任何类型的实例(包括函数类型).

> NOTE: Use `Any` and `Any` only when you explicitly need the behavior and capabilities they provide. It is always better to be specific about the types you expect to work in your code.

