Automatic Reference Counting

Swift uses ARC to track and manage your app's memory usage. In most cases, this means that memory management "just works" in Swift, and you do not need to think about memory management yourself. ARC automatically frees up the memory used by class instances when those instances are no longer needed.

* Reference Counting only applies to instance of classes. Structures and enumerations are value types, not reference types, and are not stored and passed by reference.
* Whenever you assign a class instance to a property, constant, or variable, that property, constant, or variable makes a strong reference to the instance. The reference is called a "Strong" reference because it keeps a firm hold on that instance, and does not  allow it to be deallocated for as long as that strong reference remains.

**类实例间的"强引用环"**

如何解决类实例间的"引用环"问题, Swift提供了两种方式:

* weak references
* unowned references

Weak and unowned references enable one instance in a reference cycle to refer to the other instance without keeping a storng hold on it. The instances can then refer to each other without creating a strong reference cycle.

> Use a weak reference whenever it is valid for that reference to become nil at some point during its lifetime. Conversely, use an unowned reference when you know that the reference will never be nil once it has been set during initialization.

> NOTE Weak references must be declared as variables, to indicate that their value can change at runtime. A weak reference cannot be declared as a constant.

* Variables of a nonoptional type cannot be set to nil.

* An `unowned`  reference is always defined as a nonoptional type.

* 在closure中引用了类中的属性或方法时,最好附带上`self`, 这样也是对我们的一个提醒(即这里引用了self)

**在Closures中解决closure与class instance之间的循环引用问题**

我们在closure的定义中定义一个`capture list`来解决closure与class instance之间的循环引用问题.

**Defining a Capture List**

Each item in a capture list is a pairing of the `weak` or `unowned` keyword with a reference to a class instance(such as self) or a variable initialized with wome value(such as delegate = self.delegate!).

**Optional Chaining**

  `Optional Chaining` is a process for querying and calling properties, methods, and subscripts on an optional that might currently be `nil`. Multiple queries can be chained together, and the entire chain fails gracefully if any link in the chain is `nil`.
  
* 没有返回值的func 或者 methods其实是有一个隐式的返回类型的, 实际上返回的是(),或者叫空tuple.

* Return vlaues are always of an optional type when called through optional chaining.



































