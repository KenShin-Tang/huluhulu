####Initialization

Initialization is the process of preparing an instance of a class, structure, or enumeration for use. This process involves setting an initial vaue for each stored property on that instance and performing any other setup or initialization that is required before the new instance is ready for use.

我们使用`initializers`来创建一个特定类型的实例.

**Initializers**

`Initializers` are called to create a new instance of a particular type. In its simplest form, an initializer is like an instance method with no parameters, written using the `init` keyword.

**Local and External Parameter Names**

Function 和 method中的参数, 初始化参数可以有 local name(for inner use)和 external name(for outer use).

* External names must always be used in an initializer if they are defined, and omitting them is a compile-time error.(如果有external name,那么调用的时候必须写)

**Optional Property Types**

如果自定义的类型中有一个stored property在逻辑上允许"无值"-- 或许因为在初始化期间不能设置,或者它允许在后续的情形中没有值, 我们可以declare the property with an `optinoal type`. 这样就会自动初始化为`nil`, 

**Assigning Constant Properties During Initialization**

> NOTE: For class instances, a constant property can be modified during initialization only by the class introduces it. It cannot be modified by subclass.

**Memberwise Initializers for Structure Types**

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

Swift's compiler performs four helpful safety-checks to make sure that two-phase initialization is completed without error:

*Safety check 1:* A designated initializer must ensure that all of the properties introduced by its class are initialized before it delegates up to a superclass initializer.

**Initializer Inheritance and Overriding**

Unlike subclasses in Objective-C, Swift subclasses do not inherit their superclass initializers by default. Swift's approach prevents a situation in which a simple initializer from a superclass is inherited by a more specialized subclass and is used to create a new instance of the subclass that is not fully or correctly initialized.

**Automatic Initializer Inheritance**

As mentioned above, subclasses do not inherit their superclass initializers by default. However, superclass initializers are automatically inherited if  certain conditions are met.

Assuming that you provide default values for any new properties you introduce in a subclass, the following two rules apply:

**Rule 1**

If your subclass doesn't define any designated initializers, it automatically inherits all of its superclass designated initializers.

**Rule 2**

If your subclass provides an implementation of all of its superclass designated initializers -- either by inheriting them as per rule 1, or by providing a custom implementation as part of its definition -- then it automatically inherits all of the superclass convenience initializers.


**Failable Initializers**

* You cannot define a failable and a nonfailable initializer with the same parameter types and names.
* A failable initializer creates an `optional` value of the type it initializers. You write `return nil` within a failable initializer to indicate a point at which initialization failure can be triggered.

**Failable Initializers for Enumerations**

* You can use a failable initializer to select an appropriate enumeration case based on one or more parameters. The initializer can then fail if the provided parameters do not match an appropriate enumeration case.

  Enumerations with raw values automatically receive a failable initializer, `init?(rawValue:)`, that takes a paramter called `rawValue` of the appropriate raw-value type and selects a matching enumeration case if one is found, or triggers an initialization failure if no matching value exists.
  
**Overriding a Failable Initializer**

子类可以override父类的failable initializer, 正如可以override其他initializer一样. 子类中可以用nonfailable initializer来override 父类的failable initializer. 这样我们可以使得定义的子类不会因父类允许failure而初始化失败.

* Note that if you override a failable superclass initializer with a nonfailable subclass initializer, the only way to delegate up to the superclass initializer is to force-unwrap the result of the failable superclass initializer.


**The init! Failable Initializer**

我们定义一个failable initializer来创建一个optional的instance, 通常在`init`后标记一个`?`,即`init?`.


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

















