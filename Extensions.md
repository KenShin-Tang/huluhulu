####Extensions

Extensions 用于给已有的class, structure, enumeration以及protocol增加新的"功能". 与Objective-C中的category很像,但是Swift中的extension是没有名字的.

在Swift中我们可以使用extension来:
* 添加computed instance property和computed type property
* 添加instance methods and type methods
* 添加新的 initializers
* 定义subscript
* 定义/使用新的nested types
* 使现有的类型遵从指定的protocol

> Extension

**Extension Syntax**

```Swift
extension SomeType {
  //new functionality to add to SomeType goes here
}
```
An extension can extend an existing type to make it adopt one or more protocols. Where this is the case, the protocol names are written in exactly the same way as for a class or structure:
```Swift
extension SomeType: SomeProtocol, AnotherProtocol {
  //  implemetation of protocol requirements goes here
}
```
* Extension 只能给现有类添加 computed properties, 而不能添加 stored properties 或者 property observers.
* 

