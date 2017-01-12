##Attributes

* Swift中的Attributes用来为declaration或者type提供更多的信息, 分为两种:

  1. 用于declaration的
  2. 用于types的
* 写法: 
  1. *@attribute name*
  2. *@attribute name( attribute arguments)*

有些declaration attributes 可以接收参数, 这些参数描述了更多关于attribute的信息以及如何它如何用于特定的declaration. 这些参数包括在圆括号中, 并且格式也是由所属的attribute定义的.

* Declaration Attributes:
  
  1. `available(参数列表)`: 参数间以逗号分开,用来指代此声明的适用范围,由参数表明(参数可以是`iOS/iOSApplicationExtension/OSX/OSXApplicationExtension/watchOS/watchOSApplication/tvOS/tvOSApplicationExtension`, 也可以用`*`指代以上所有的平台.后面就可以跟`unavailable/introduced(如果列表中只有此参数key,可省略): version_name/deprecated:  version_name/obsoleted(淘汰,过时的): version_name/message(编译警告或错误信息): message_name/renamed(此声明被重命名了): new_name/等
  2. `objc`:用来指代此代码可以与OC混编,Apply this attribute to any declaratino that can be represented in Objective-C.比如,非嵌套的class, protocol, 非泛型枚举, 类的properties以及方法(包括getter和setter), protocol, initializer, deinitializer, 以及subscripts.其告诉编译器这个声明是可以与OC混编的. 
   
   使用`objc`修饰的类必须继承自OC中的class. 如果将`objc`用于class或者protocol, 它会隐式地将之用之于OC中相应的class或者protocol的成员. 也会隐式地将之用之于继承自有`objc`修饰的类或者OC中的类. `objc`修饰的protocol不能继承于没有`obj`修饰的protocl.
   
   如果`objc`修饰枚举类型, 每个枚举的case就会对应OC代码的 枚举类型名+case名, 首字母大写. 比如Swift中`Planet`枚举类型中有一个case为`venus`,那么在OC中就会转换为`PlanetVenus`.
   
   `ojbc` attribute可以接收单参数, 用来组成id. 对应于Swift中`objc`修饰的实体(类名, 枚举类型名, 枚举case名, protocol名, 方法名, 构造器名),当你想要其在OC中使用一个不同的名字表示. 比如:
```Swift
@objc
class ExampleClass: NSObject {
    var enalbed: Bool {
      @objc(isEnable) get {
        // Return the appropriate value
        }
    }
}
```
  3. `nonescape`: apply this attribute to a function or method declaration to indicate that a parameter will not be stored for later execution, such that it is guaranteed not to outlive the lifetime of the call.
  4. `nonobjc`: 告诉编译器不允许此代码用于OC中,即不可与OC混编.`nonobjc`修饰的方法不能覆盖`objc`修饰的方法, 反之则可以.同样的, 如果protocol中有要求`objc`修饰的方法, 那么`nonobjc`修饰的方法就不能satisfy这个protocol.
  5. `NSApplicationMain`: 用来指明其修饰的类作为application delegae.相当于调用`NSApplicationMain(_:_:)`函数(即macOS应用的入口主函数). 如果不用这个attribute, 可以写一个`main.swift`文件, 其内容为
    ```Swift
    import AppKit
    NSApplicationMain(CommandLine.argc, CommandLine.unsafeArgv)
    ```
    
  6. `NSCopying`: 类似OC中的`copy` attribute.
  7. `NSManaged`:
  8. `testable`: 
  9. `UIApplicationMain`: 用来指明其修饰的类作为application delegate.用于与`NSApplicationMain`类似.
  10. `warn_unused_result`:optionally accepts one of the two attribute arguments:
    * message=*message*
    * mutable=*method_name*
  11. `discardableResult`:用于有返回值的函数或者方法的声明, 当调用此函数或方法而没有使用它的返回值时,会发出编译警告.
  12. `GKInspectable`:

* Declaration Attributes Used by Interface Builder

Interface Builder attributes are declaration attributes used by Interface Builder to synchroize with Xcode: IBAction, IBDesignable, IBInspectable, IBOutlet. 与OC中类似, 我们用`IBOutlet`和`IBInspectable`来修饰class的propertise. 使用`IBAction`修饰class的method, `IBDesignable`修饰类.

* Type Attributes

  1. `autoclosure`: 自动将一个expression转化为闭包. 将之用与函数或者方法声明中修饰参数类型(这个类型是没有参数只返回expression本身的值的函数类型).
  2. `convention`:
  3. `escaping`:























