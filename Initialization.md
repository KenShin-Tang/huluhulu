####Initialization

Initialization就是class, structure, or enumeration用来做初始化的过程. 但是与 OC 不同的是, 它不返回值,而只是做初始化工作. 对应`initializer`, 我们也可以定义一个`deinitializer`

我们使用`initializers`来创建一个特定类型的实例.

### Setting Initial Values for Stored Properties

Class 和 structure 必须在实例创建完成前对所有的 stored property 赋初值. 我们要么在 stored property 声明时就赋初值, 要么就在 initializer 中进行初始化.

我们可以在 initializer 中为 stored property 设置初始值或者在 property 的定义中直接赋 default property value.

> 注意: 当我们 在声明或者 initializer中给 stored property 赋初值时, 是直接设置的, 不会导致调用其 property observer 的.

**Initializers**

`Initializers` 使用关键字 `init`来标识, 参数可有可无.

### **Parameter Names and Argument Labels**

* 与 function 和 method 一样, initializer 的 parameters会有 parameter name for use in initializer's body and an argument label for use when calling the initializer.

* 由于 initializer 不会有明确的函数名, 所以 initializer 的 parameter 的 name 和 type 就扮演一个方法或函数"ID"的角色. 默认地, Swift 会为 initializer 的 parameter默认生成 argument label(当然我们也可以手动指定).

**Optional Property Types**

如果自定义的类型中有一个stored property在逻辑上允许"无值"-- 或许因为在初始化期间不能设置,或者它允许在后续的情形中没有值, 我们可以declare the property with an `optinoal type`. 这样就会自动初始化为`nil`, 

**Assigning Constant Properties During Initialization**

> NOTE: For class instances, a constant property can be modified during initialization only by the class introduces it. It cannot be modified by subclass.

#### Default Initializer

* 对于 class 和 structure, 只要对所有的 properties 都有初始值, 即使我们没有显式地提供 initializer, Swift 也会为我们默认地生成一个 default initializer.

```Swift
	class ShoppingListItem {
		var name: String?
		var quantity = 1
		var purchased = false
    }
    var item = ShoppingListItem()
```

#### **Memberwise Initializers for Structure Types**

Structure types automatically receive a `memberwise initializer` if they do not define any of their own custom initializers. Unlike a default initializer, the structure receives a memberwise initializer even if it has stored properties that do not have default values.

**Initializer Delegation for Value Types**

Initializers can call other initializers to perform part of an instance's initialization. This process, known as `initializer delegation`, avoids duplcating code across multiple initializers.

**Class Inheritance and Initialization**

All of a class's stored properties -- including any properties the class inherits from its superclass -- must be assigned an initial value during initialization.

**Designated Initializers and Convenience Initializers**

A **designated** initializer fully initializers all properties introduced by that class and calls an appropriate superclass initializer to continue the initialization process up the superclass chain.

Every class must have **at least one** designated initializer.

**Convenient** initializers are secondary, supporting initializers for a class. You can define a convenience initializer to call a designated initializer from the same class as the convenience initializer with some of the designated initializer's parameters set to default values.

**Syntax for Designated and Convenience Initializers**

Designated initializers:
```Swift
init(parameters) {
  //statements
}
```

Convenience initializers:
```Swift
convenience init(parameters) {
  //statements
  }
```

**Two-Phase Initialization**

In first phase, each stored property is assigned an initial value by the class that introduced it. Once the initial state for every stored property has been determined, the second phase begins, and each class is given the opportunity to customize its stored properties further before the new instance is considered ready for use.

Swift 的编译器会对初始化工作进行四方面的检查以确保初始化工作无误地完成. 

* Safety check 1: Designated initializer  需确保在委托给父类之前自己引入的 property 都已初始化.
	
	As mentioned above, the memory for an object is only considered fully initialized once the initial state of all of its stored properties is known. In order for this rule to be satisfied, a designated initializer must make sure that all of its own properties are initialized before it hands off up the chain.
	
* Safety check 2: designated initializer在给继承来的property 赋值之前必须先委托父类做完初始化,否则(即在之后)继承来的 property赋的新值就会被其 superclass 的 initializer 覆盖重写.

* Safety check 3: A conveninece initializer must delegate to another initializer before assigning a value to any property(including properties defined by the same class). If it doesn't, the new value the convenience initializer assigns will be overwritten by its own class's designated initializer.

* Safety check 4: An initializer cannot call any instance methods. read the value of any instance properties, or refer to `self` as a value until after the first phase of initialization is complete.

**Initializer Inheritance and Overriding**

与 OC 不同, Swift 子类不会默认地继承父类的 initializer. 是为了防止父类的 initializer 不能正确地/不完整地 initialize 子类的实例.

**Automatic Initializer Inheritance**

之前提到过, 子类默认不会继承父类的 initializer. 然而, 在特定情况下, 父类的 initializer 是会自动被子类继承的.

假定子类为每一个它自己引入的 property 设置了默认值, 那么下面两个准则就适用:

**Rule 1**

如果子类没有定义任何designated initializers, 那么它就自动继承父类的designated initializers.

**Rule 2**

如果子类实现了父类所有的 designted initailizers(即使是 子类中作为 convenience initializer).-- 要么是通过 rule1中所述方式实现或者在其定义中"实际"实现的.那么子类就默认继承所有的父类的 convenience initializer.


#### **Failable Initializers**

* 使用`init?`标识此 initializer 为 failable.
* You cannot define a failable and a nonfailable initializer with the same parameter types and names.
* A failable initializer creates an `optional` value of the type it initializers. You write `return nil` within a failable initializer to indicate a point at which initialization failure can be triggered.

> 注意: 严格来讲, initializer 是没有返回值的.它的职责就是确保`self`完全正确地初始化了. 我们`return nil` 是为了表明 a point at which initialization failure can be triggered, 成功的情况下是不需要 return "something" 来指明的.



**Failable Initializers for Enumerations**

* You can use a failable initializer to select an appropriate enumeration case based on one or more parameters. The initializer can then fail if the provided parameters do not match an appropriate enumeration case.

  Enumerations with raw values automatically receive a failable initializer, `init?(rawValue:)`, that takes a paramter called `rawValue` of the appropriate raw-value type and selects a matching enumeration case if one is found, or triggers an initialization failure if no matching value exists.
  
**Overriding a Failable Initializer**

子类可以override父类的failable initializer, 正如可以override其他initializer一样. 子类中可以用nonfailable initializer来override 父类的failable initializer. 这样我们可以使得定义的子类不会因父类允许failure而初始化失败.

* Note that if you override a failable superclass initializer with a nonfailable subclass initializer, the only way to delegate up to the superclass initializer is to force-unwrap the result of the failable superclass initializer.


**The init! Failable Initializer**

我们定义一个failable initializer来创建一个optional的instance, 通常在`init`后标记一个`?`,即`init?`. 当然我们也可以创建一个


**Required Initializers**

Write the `required` modifier before the definition of a class initializer to indicate that every subclass of the class must implement that initializer:
```Swift
class SomeClass {
  required init() {
  // initializer implementation goes here
  }
}
```
在override一个required的designated initializer的时候, 不用写override.

**Setting a Default Property Value with a Closure or Function**

```Swift
class SomeClass {
  let someProperty: SomeType = {
  // create a default value for someProperty inside this closure
  // someValue must be of the same type as SomeType
  return someValue
}()
```
注意: closure 末尾有一对圆括号, 这就是告诉 Swift 立即执行这个 closure. 如果没有这对括号, 我们则是要将整个 closure 本身赋值给这个 property, 而不是这个 closure 的返回值.
> 当我们使用 closure初始化某一个 property 时, 这个实例其他内容还不确定是否已经初始化完成了, 所以我们还不能在 closure 中访问其他的 property, 即使有的property有默认值(但是为了保险, Swift 还是不允许访问). 即使是`self` 也不行.

















