####Generics(泛型)
`Generics code` enables you to write flexible, reusable functions and types that can work with any type, subject to requirements that you define.

Generics are one of the most powerful features of Swift.

**Generics解决的问题**
我们交换两个值, 一般来说我们会
```Swift
func swapTwo***(inout a: Type, inout _ b: Type) {
  }//
  ```
我们通常要指明要处理的数据的类型,但是我如果想要交换两个数字 或者字符串,或者字典, 那么我们就必须分别为各个类型定义一个`swapTwo***(inout a: Type, inout _ b: Type)` 形式的函数来处理, 这样不是很恶心吗? 明明它们的区别 仅仅在于不同的类型参数而已其实做的操作是一样的即交换两个参数的指针.  那么`泛型(Generics`就是用来解决这样问题而生的, 我们可以定义一个通用的函数, 它可以用在任意类型的数据上.

例子:
```Swift
func swapTwoValue<T>(inout a: T, inout _ b: T) {
  let temporatyA = a
  a = b
  b = temporary
  }// T(当然也可以写其他字母)是一个`占位符类型`(placeholder type)它可以代表任何类型
  ```
**Tyep Parameters**

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

我们需要对一些泛型进行约束(比如类型必须是继承资某个类或者遵从某个协议等.