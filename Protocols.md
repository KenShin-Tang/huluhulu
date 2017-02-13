####Protocols

A `protocol` defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol can then be adopted by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to conform to that protocol.

**语法**

```Swift
protocol SomeProtocol {
  // protocol definition goes here
}
```
自定义类型要遵从某些protocol, 只需将protocol的名字置于类型名的后面用分号隔开,比如
```Swift
struct SomeStructure: FirstProtocol, AnotherProtocol {
  // structure definition goes here 
}

```

**Protocols as Types**

* protocol 本上就是一种类型(所以首字母要大写哦);
* 可以作为函数中/方法中/ initializer 中的参数类型, 返回值类型;
* 可以作为常量/变量/属性的类型;
* 作为容器类中的元素.

> NOTE: Types do not automatically adopt a protocol just by satisfying its requirements. They must always explicitly declare their adoption of the protocol.

**Class-Only Protocols**

```Swift
protocol SomeClassOnlyProtocol: class, SomeInheritedProtocol {
  //class-only protocol definition goes here 
}
```

### Class Implementations of Protocol Initializer Requirements

* 类实现的 protocol方法需要在方法前添加`required`关键字(这样就能提示此类或者其子类 conform to 相应的方法.(说道这里, 那么` final` 修饰的 class 就不必写` required` 了. 因为它不能被继承.
* 如果子类重写了父类的 designated initializer, 且同时也实现了遵循的 protocol 中的 initializer requirement同样的方法, 那么同时要使用`required override`来修饰.

> NOTE: Use a class-only protocol when the behavior defined by that protocol's requirements assumes or requires that a conforming type has reference semantics rather than val<!---->ue semnatics.

### Adding Protocol Conformance with an Extension

* 如果类型实际上实现了某个 protocol 的所有 requirements, 但是没有声明其遵循了某个 protocol, 我们可以使用`extension ComformingType: Protocol {}` 来表明.

### Protocol Inheritance

* protocol能够多继承并且能够添加新的 requirements.
* 我们可以限制 protocol 只适用于 class, 写法是在 protocol的继承列表中第一个位置添加` class` 关键字.

**Protocol Composition**

*Protocol compositions* have the from `protocol<SomeProtocol, AnotherProtocol>`

* 我们可以合并protocol requirement 为单个 requirement, 写法是 protocol由`&`连接起来. 注意这种并不是定义了一种新的 protocol 类型, 它仅仅是定义了一个`temporary local protocol`.
* 
 
> NOTE: Protocol compositions do not define a new, permanent protocol type. Rather, they define a temporary local protocol that has the combined requirements of all protocols in the composition.

** Checking for Protocol Conformance**

`is` and `as`:
* The is operator returns `true` if an instance conforms to a protocol and returns `false` if it does not.
* The `as?` version of the downcast operator returns an optional value of the protocol's type, and this value is `nil` if the instance does not conform to that protocol.
* The `as!` version of the downcast operator forces the downcast to the protocol type and triggers a runtime error if the downcast does not successed.

**Optional Protocol Requirements**(这个只有在与 OC混编的时候才会有)

* 我们通常使用`optional`前缀修饰符来指明protocol中的method或者property是optional的(同时我们必须在protocol前面加上`@objc`.
* protocol 中的 optional requirement 中的 method 或者 property是 optional 的, 那么这个 method 或者property 本身的类型就自动变成一个 optional 的, 比如(Int) -> String 会变成 ((Int) -> String)?.
* 

> NOTE: Optional protocol requirements can only be specified if your protocol is amred with the @objc attribute. This attribute indicates that the protocol should be exposed to Objective-C code. Even if you are not interoperating with Objective-C, you need to mark your protocols with the @objc attribute if you want to specify optional requirements. 
> Note that @objc protocols can be adopted only by classes that inherit from Objective-C classes or other @objc classes. They can't be adopted by structures or enumeratoins.

> NOTE: Strictly speaking, you can write a custom class that conforms to CounterDataSource without implementing either protocol requirement. They are both optional, after all. Although technically allowed, this wouldn't make for a very good data source.

**Protocol Extensions**

Protocols可以用来拓展以便为 comforming types提供method 和 property 的实现.这就使得我们可以定义一些 protocol 的 behavior, 而不是将这些 behavior 分布到各个 comforming type或 global function 中去实现.

**Protocol Default Implementations**

我们可以利用 protocol extension 来为 protocol 的 method 或者 property 提供默认的实现. 如果 Comforming type 又实现了这些 methods 或者 properties, 则默认的实现会被替换.

> 注意, 我们可能注意到一旦 protocol 提供了Default Implementations, 意味着 Comforming type 可以不写 implementation, 但是它实际上是有Default Implementation 的, 这与前面的 optional protocol requirements是不同的.


#### Adding Constrains to Protocol Extensions

当然 extension有时也是有条件的, 不能谁都能 conform 的(那岂不是太随便了😀), 所以我们就可以为 extension 添加一些 constraints, 以下是写法:

``` Swift
extension Collection where Iterator.Element: TextRepresentable {
	var textualDescription: String {
		let itemsAsText = self.map { $0.textualDescription }
		return "[" + itemsAsText.joined(seperator: ", " + "]"
	}
}
```
> NOTE: 
	If a conforming type satisfies the requirements for multiple constrained extensions that provide implementations for the same method or property. Swift will use the implementation corresponding to the most specialized constraints.























