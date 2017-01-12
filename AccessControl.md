####Access Control

**Modules and Source Files**

Swift's access control model is based on the concept of modules and source files.

A `module` is a single unit of code distribution - a framework or application that is built and shipped as a single unit and that can be imported by another module with Swift's import keyword.

A `source file` is a single Swift source code file within a module(in effect, a single file within an app or framework). Although it is common to define individual types in separate source files, a single source file can contain definitions for multiple types, functions, and so on.

Swift中有三种级别的access level
* Public access:任何导入其所在module的源文件都可以使用
* Internal access: 只能在被所在的module中的代码使用
* Private access: 只能在所在的source file的代码使用.

Swift中的access levels遵循一个总的规则就是: 高级别的entity不能定义在低级别(更严格)的entity中:
* 一个public variable 不能为internal或者private的类型,因为public的类型可以在任何地方调用而private的却不能.
* 一个function不能比它的参数或者返回值的类型的access level还要高, because the function could be used in situation where its constituent types are not avaliable to the surrounding code.

**Default Access Levels**

All entities in your code(with a few specific exceptions, as described later in this chapter) have a default access level of internal if you do not specify an explicit access level yourself. As a result, in many cases you do not need to specify an explicit access level in your code.

**Access Levels for Single-Target Apps**

When you writea simple single-target app, the code in your app is typically self-contained within the app and does not need to be made avaliable outside of the app's module. The default access level of internal already matches this requirement. Therefore, you do not need to specify a custom access level. You may, however, want to mark some parts of your code as private in order to hide their implemetation details from other code within the app's module.

**Access Levels for Frameworks**

When you develop a framework, mark the public-facing interface to that framework as public so that it can be viewed and accessed by other modules, such as an app that imports the framework. This public-facing is the application programming interface(or API) for the framework.

**Access Levels for Unit Test Targets**

When you write an app with a unit test target, the code in your app needs to be make available to that module in order to be tested. By default, only entities marked as public are accessible to other modules. However, a unit test target can access any internal entity, if you mark the import declaration for a product module with the `@testable` attribute and compile that product module with testing enabled.

**Access Control Syntax**

```Swift
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

tuple的access level是tuple中所有"元"中level最低的,即最restrictive的.
> NOTE Tuple types do not have a standalone definition in the way that classes, structures, enumerations, and functions do. A tuple type's access level is deduced automatically when the suple type is used, and cannot be specified explicitly.

**Function Types**

类似地, function的access level是所有参数及返回值中最restrictive的那个级别.

如果上下文(即默认的)function的access level与推断值(即所有参数及返回值中最restrictive的那个级别)不匹配,那么我们必须显式地指定.

**Enumeration Types**

所有的case的Access level都与Enumeration type本身一致, 不能单独指定. 其中的raw value 和 associated value的access level不能比enumeration的level低.

**Nested Types**

同理, 默认的都是若外部private, 嵌套的也自动为private; 若外部public或internal,嵌套的类型自动internal, 如需指定需要显式声明.

**Subclassing**

子类不能比父类的access level高. 然而我们可以override任何在特定的access context中可见的类成员(method, property,initializer, subcript). 这就意味着我们可以将父类中一个private的method在子类中override为internal的. 比如
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


































