# Automatic Reference Counting

Swift 使用ARC 来追踪管理app 的内存. 这就意味着多数情境下, ARC在 Swift 中正常"工作", 我们无需过多关注内存管理. ARC 会自动将不再使用的 instance 内存清空.

* 引用计数技术只适用于引用类型(即 class) 而不适用于值类型(如 structure, enumeration).
* ARC 会自动追踪每一个 class instance有多少个 properties, constants以及 variables 正在引用它, 只要 instanec有引用存在, 它就不会被销毁.
* 只要我们将一个 class intance 赋值给某个property, constant或者 variable, 那么这些个 property/ constant/ variable 就会持有一个此 instance 的" strong reference". 这个 reference 之所以是"strong reference" 是因为它在两者之间建立了一个稳定的持有/被持有关系, 只要存在就不允许被引用的instance的被销毁.

### ARC in Action

**类实例间的"强引用环"**

如何解决类实例间的"引用环"问题, Swift提供了两种方式:

* weak references
* unowned references

Weak and unowned references使得"引用环"中的一个 instance  无需"强引用"另一个 instance. 这样就可以在两者之间建立一个非"强引用环".

> Use a weak reference whenever it is valid for that reference to become nil at some point during its lifetime. Conversely, use an unowned reference when you know that the reference will never be nil once it has been set during initialization.

> NOTE Weak references must be declared as variables, to indicate that their value can change at runtime. A weak reference cannot be declared as a constant.

* Variables of a nonoptional type cannot be set to nil.

* An `unowned`  reference is always defined as a nonoptional type.

* 在closure中引用了类中的属性或方法时,最好附带上`self`, 这样也是对我们的一个提醒(即这里引用了self)

### Strong Reference Cycles for Closures

由于 Closure 是引用类型, 所以与 class 之间就存在潜在的"强引用环"问题.


**在Closures中解决closure与class instance之间的循环引用问题**

我们在closure的定义中定义一个`capture list`来解决closure与class instance之间的循环引用问题.

**Defining a Capture List**

Each item in a capture list is a pairing of the `weak` or `unowned` keyword with a reference to a class instance(such as self) or a variable initialized with some value(such as delegate = self.delegate!).

#### Weak and Unowned References

那么 closure 与  instance 间相互引用时, 该用` unowned` 呢还是` weak` 呢?

* 如果 closure 与  它捕获的引用间总是相互引用且最终同时销毁, 那么我们可以使用` unowned`;
* 相反地, 如果捕获的引用有可能为 nil 时, 使用` weak` 修饰.

**Optional Chaining**

  `Optional Chaining` is a process for querying and calling properties, methods, and subscripts on an optional that might currently be `nil`. Multiple queries can be chained together, and the entire chain fails gracefully if any link in the chain is `nil`.
  
* 没有返回值的func 或者 methods其实是有一个隐式的返回类型的, 实际上返回的是(),或者叫空tuple.

* Return vlaues are always of an optional type when called through optional chaining.

### 总结:

* 两个`optional`的对象关联在一起, 可以使用`weak` 打破潜在的"强引用环";
* 一个 optional 和一个 nonoptional 关联在一起要分情况:
	* 如果其中一个可以为 nil 而另一个不能为 nil( 且不能为 nil 的 property instance生命周期要长一些, 比如银行卡与持卡人的关系, 银行卡的持卡人 property的生命周期要比卡长,所以 给这个 property 添加 `unowned` 修饰符来确保不会造成"强引用环").
	* 如果在初始化完成后, 两者都一直有值, 那么我们就可以使用 `unowned` + `!`(implicitly unwrapping optional) 来确保不会造成"强引用环".































