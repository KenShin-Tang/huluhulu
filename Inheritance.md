####Inheritance

A class can `inherit` methods, properties, and other characteristics from another class. 

Inheritance is a fundamental behavior that differentiates classes from other types in Swift.

**Defining a Base Class**

Any class that does not inherit from another class is known as a base class.

> NOTE:Swift classes do not inherit from a universal base class. Classes you define without specifying a superclass automatically bacome base classes for you to build upon.

**Overriding**

A subclass can probide its own custom implementation of an instance method, type method, instance property, type property, or subscript that it would otherwise inherit from a superclass. This is called `Overriding`.

To override a characteristic that would otherwise be inherited, you prefix your overriding definition with the `override` keyword.

**Accessing Superclass Methods, Properties, and Subscripts**

you access the superclass version of a method,  property, or subscript by  using the `super` prefix:
  * An overridden method named `someMethod()` can call the superclass version of someMethod() by calling `super.someMethod()` within the overriding method implementation.
  * An overridden property called `someProperty` can access the superclass version of someProperty as `super.someProperty` within the overriding getter or setter implementation.
  * An overridden subscript for `someIndex` can access the superclass version of the same subscript as super[someIndex] from within the overridding subscript implementation.
 
* 父类中的属性的`读写`attribute在子类中只能被增强,即父类中的read-write属性在subclass不能是read-only, 而父类中的read-only属性在subclass可以override为 read-write.
* overriding setter时, 我们也必须override getter.如果无需修改getter的实现, 可以在getter中调用`super.someProperty`.
* we cannot add property observers to inherited constant stored properties or inherited read-only computed properties.(**可以叫它们Immutable property**)

* 不能同时为一个property既override其setter又override它的perperty observer, 因为这是多余的, 我们在setter中就可以知道什么时候property的value要变了.

**Preventing Overrides**

我们可以使用`final` 修饰符来防止 method, property, subscript被覆写.

我们使用`final class`来指明此class是一个究级类,不能再被继承了. 






















