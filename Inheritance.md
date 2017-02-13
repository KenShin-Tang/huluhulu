####Inheritance

就是通常的继承, 但是 Swift 中可以给继承来的 property 添加 observer, 不管它是否是当前类 introduce 的.

Inheritance is a fundamental behavior that differentiates classes from other types in Swift.

**Defining a Base Class**

基类(不继承自任何类的类).

> NOTE:Swift classes do not inherit from a universal base class. Classes you define without specifying a superclass automatically bacome base classes for you to build upon.

**Overriding**

使用 `override` 关键字表明重写.

**访问父类的Methods, Properties, and Subscripts**

使用 `super` 前缀:
  * An overridden method named `someMethod()` can call the superclass version of someMethod() by calling `super.someMethod()` within the overriding method implementation.
  * An overridden property called `someProperty` can access the superclass version of someProperty as `super.someProperty` within the overriding getter or setter implementation.
  * An overridden subscript for `someIndex` can access the superclass version of the same subscript as super[someIndex] from within the overridding subscript implementation.
 
* 父类中的属性的`读写`attribute在子类中只能被增强,即父类中的read-write属性在subclass不能是read-only, 而父类中的read-only属性在subclass可以override为 read-write.
* overriding setter时, 我们也必须override getter.如果无需修改getter的实现, 可以在getter中调用`super.someProperty`.
* we cannot add property observers to inherited constant stored properties or inherited read-only computed properties.(**可以叫它们Immutable property**)

* 不能同时为一个property既override其setter又override它的perperty observer, 因为这是多余的, 我们在setter中就可以知道什么时候property的value要变了.

**Preventing Overrides**

我们可以使用`final` 修饰符来防止 method, property, subscript被重写.

我们使用`final class`来指明此class是一个究级类,不能再被继承了. 






