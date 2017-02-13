####Generics(泛型)
`Generics code` 可以使得我们写出更灵活, 可复用, 更通用的 function 和 types 用于"合规类型".

Generics are one of the most powerful features of Swift, and much of the Swift standard library is built with generic code. In fact, you've been using generics even if you didn't realize it. For example, Swift's `Array` and `Dictionary` types are both generic collections. You can create an array that holds `Int` values, or an array that holds `String` values, or indeed an array for any other that can be created in Swift. Similarly, you can create a dictionary to store values of any specific type, and there are no limitions on what that type can be.

**Generics解决的问题**

我们交换两个值, 一般来说我们会
```Swift
func swapTwo***(inout a: Type, inout _ b: Type) {
  }//
  ```
我们通常要指明要处理的数据的类型,但是我如果想要交换两个数字 或者字符串,或者字典, 那么我们就必须分别为各个类型定义一个`swapTwo***(inout a: Type, inout _ b: Type)` 形式的函数来处理, 这样不是很低效吗? 明明它们的区别 仅仅在于不同的类型参数而已其实做的操作是一样的即交换两个参数的指针.  那么`泛型(Generics`就是用来解决这样问题而生的, 我们可以定义一个通用的函数, 它可以用在任意类型的数据上.

例子:
```Swift
func swapTwoValue<T>(inout a: T, inout _ b: T) {
  let temporatyA = a
  a = b
  b = temporary
  }// T(当然也可以写其他字母)是一个`占位符类型`(placeholder type)它可以代表任何类型
  ```
  
### Generic Function

* 使用` placeholder type name`(占位类型名)
* 占位类型不代表任何实际的类型, 只是起到"占位"作用, 即是某个类型.

**Type Parameters**

* type parameter 不限于一个, 我们可以是`<>`中写多个 type parameter, 以都好隔开.

**Naming Type Parameters**
大多数情况下, type parameters都有一个表意的name, 如Dictionary<Key, Value>中的`Key`和`Value` ,  Array<Element> 中的`Element`.

**Generic Types**

**Type Constraints**
```Swift
func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
  //function body goes here
}
```

**泛型约束**

我们需要对一些泛型进行约束(比如类型必须是继承资某个类或者遵从某个协议等).

### Associated Types

我们有时在定义 protocol 可能会需要关联一些类型, 但是类型的"本尊"可能我们事先并不知晓, 但是呢我们又需要引用这些类型, 为达到这个目的, 我们可以使用` associatedtype` 关键字后 指明 其后的 typename 是一个关联类型, 那些 conforming type到时会指明的.