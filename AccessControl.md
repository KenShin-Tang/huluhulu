####Access Control

**Modules and Source Files**

Swift's 中的access control model 是基于 modules and source files概念上的.

A `module` 即一个独立的代码分发单元.比如一个独立编译的并可以由其他 module 导入的(import)framework 或者 application.

A `source file` 是一个 module( framework 或者 application) 中单独的 Swift 源代码文件. 一个源代码文件中可以定义一个或者多个 types, functions 等等.

Swift中对 entities有五种级别的access level

* `open` 和 `public` :entities所属的 module 以及任何导入其所属module的源文件都可以使用
* `internal`: 只能在被所在的module中的代码使用;
* `fileprivate`: 只能被其所属的 source file访问;
* `private`: 只能在entity所在的声明范围内才可以使用.

`Open` 是最宽松的access level, `private` 是最严格的(最低的)的 access level.

`Open`只能用于 classes 以及 class members, 并且与` public` 有以下区别:

* `public` 修饰的或者更严格的 access level 的 classes只能在其所属的 module 中被继承.
* `public` 修饰的或者更严格的 access level 的 class members 只能在其所属的 module 中被 overriden.
* `open` classes 则可以在其所属或者导入其所属的 module 中被继承.
* `open` class memebers 则可以在其所属或者导入其所属的 module 中被 overriden.

#### 定义 access level 的原则

Swift中的access levels遵循一个总的规则就是: 高级别的entity不能定义在低级别(更严格)的entity中, 比如:
* 一个`public`的变量不能为internal/private/file-private的类型,因为public的类型可以在任何地方调用而private的却不能.
* 一个function不能比它的参数或者返回值的类型的access level还要高(更宽松), 因为这个 function 可能被用在其成分(比如参数)不可访问的情形.

**Default Access Levels**

默认地, 所有的代码中的 entity 都是`internal` 级别的 access level.( 当然也有例外, 稍后讨论). 多数情况下我们无需特别设置entity 的 access level.

**Access Levels for Single-Target Apps**

对于Single-target app,  app 的代码基本都是自包含在 app 中而不需要暴露给此module 外的. 默认的`internal` access level 已经满足了要求.因此没有必要额外设置一个 access level. 当然我们也可以使用` private` 在module中来隐藏一些实现细节.

**Access Levels for Frameworks**

 开发Framwork 时通常将 public-facing interface 的 access level 设置为`public`或者`open`以便可以被其他 modules 访问. This public-facing is the application programming interface(or API) for the framework.

**Access Levels for Unit Test Targets**

在进行单元测试时, 我们的代码需要对 unit test target module 可见. 默认地,只有` open` 和 `public` 的 entities 才可以被其他 modules 访问. 特别地,   只要我们在引入相应 module 对其标注为`@testable` 并compile that product module with testing enabled.

**Access Control Syntax**

```swift
public class SomePublicClass {}
internal class SomeInternalClass {} // Dafault,我们可以省略internal
private class SomePrivateClass {}

public var somePublicVariable = 0
internal let someInternalConstant = 0 // Dafault,我们可以省略internal
private func somePrivateFunction() {}
```
**Custom Types**

如果需要为一个自定义的类型指定access level, 我们可以在其定义的地方来实现. 比如 如果我们定义了一个`private`级别的class, 那么这个class只能在其所定义的源文件中用作某个property的类型, 一个function的参数或者返回值的类型.

类型的access level也对其内部的"成员"(比如其properties, methods, initializers以及subscripts)有影响: 即"覆盖", 若private,则默认都private, 若internal或public,则默认都internal. 如果需要对某个成员指定,必须显式地mark.

**Tuple Types**

tuple的access level是tuple中所有"元"中level最低的,即 most restrictive.
> NOTE Tuple types do not have a standalone definition in the way that classes, structures, enumerations, and functions do. A tuple type's access level is deduced automatically when the suple type is used, and cannot be specified explicitly.

**Function Types**

类似地, function的access level是所有参数及返回值中 most restrictive level.

如果根据上下文默认的function的access level与推断值(即所有参数及返回值中 most restrictive level)不匹配,那么我们必须显式地指定.

**Enumeration Types**

所有的case的Access level都与Enumeration type本身一致, 不能单独指定. 其中的raw value 和 associated value的access level不能比enumeration的level低.

**Nested Types**

同理, 默认的都是若外部private, 嵌套的也自动为private; 若外部public或internal,嵌套的类型自动internal, 如需指定需要显式声明.

**Subclassing**

子类不能比父类的access level高. 但我们可以override任何在特定的access context中可见的类成员(method, property,initializer, subcript). 这就意味着我们可以将父类中一个private的method在子类中override为internal的. 比如
```Swift
public class A {
  private func someMethod() {}
}

internal class B: A {
  override internal func someMethod() {}
}
//甚至
internal class B: A {
  override internal func someMethod() {
    super.someMethod()//在internal里面调用private
 }
```
**Constants, Variables, Properties, and Subscripts**

A constant, variable, or property cannot be more public than its type, It is not valid to write a public property with a private type, for example. Similarly, a subscript cannot be more public than either its index type or return type.

**Getter and Setters**

Getters and Setters for constants, variables, properties, and subscripts automatically receive the same access level as the constant, variable, property or subscript they belong to.

You can give a setter a lower access level than its corresponding getter, to restrict the read-write scope of that variable, property, or subscript. You assign a lower access level by writtig`private(set)` or `internal(set)` before the `var` or `subscript` introducer.

**Intializers**

Custom initializers can be assigned an access level less than or equal to the type that they initialize. The only exception is for required initializers. A required initializer must have the same access level as the class it belongs to.

**Default Initializers**

Swift自动为结构体和没有自行提供initializer且所有的properties都有默认值的class提供了一个不带任何参数的`default initializer`.

Default initializer与它所初始化的类型的Access level是同级的,除非锁初始化的类型为public的(这种情况下, default initializer是internal的).如果需要public type有一个可以被其他modle使用的无参initializer, 我们需要明确定义一个.

**Default Memberwise Initizalizer for Structure Types**

The default memberwise initializer for a structure type is considered private if any of the structure's stored properties are private. Otherwise, the initializer has an access level of internal.

**Protocols**

**Extensions*


































