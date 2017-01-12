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

**Protocols as Types**

* As parameter type or return type in a function, method, or initializer
* As the type of a constant, variable, or property
* As the type of items in an array, dictionary, or other container

> NOTE: Types do not automatically adopt a protocol just by satisfying its requirements. They must always explicitly declare their adoption of the protocol.

**Class-Only Protocols**

```Swift
protocol SomeClassOnlyProtocol: class, SomeInheritedProtocol {
  //class-only protocol definition goes here 
}
```

> NOTE: Use a class-only protocol when the behavior defined by that protocol's requirements assumes or requires that a conforming type has reference semantics rather than value semnatics.

**Protocol Composition**

*Protocol compositions* have the from `protocol<SomeProtocol, AnotherProtocol>`
 
> NOTE: Protocol compositions do not define a new, permanent protocol type. Rather, they define a temporary local protocol that has the combined requirements of all protocols in the composition.

** Checking for Protocol Conformance**

`is` and `as`:
* The is operator returns `true` if an instance conforms to a protocol and returns `false` if it does not.
* The `as?` version of the downcast operator returns an optional value of the protocol's type, and this value is `nil` if the instance does not conform to that protocol.
* The `as!` version of the downcast operator forces the downcast to the protocol type and triggers a runtime error if the downcast does not successed.

**Optional Protocol Requirements**

* These requirements do not have to be implemented by types that conform to the protocol. 我们通常使用`optional`前缀修饰符来指明protocol中的method或者property是optional的(同时我们必须在protocol前面加上`@objc`.
When you use a method or property in an optional requirement, its type auromatically becomes an optional.

> NOTE: Optional protocol requirements can only be specified if your protocol is amrked with the @objc attribute. This attribute indicates that the protocol should be exposed to Objective-C code. Even if you are not interoperating with Objective-C, you need to mark your protocols with the @objc attribute if you want to specify optional requirements. *Note that @objc protocols can be adopted only by classes that inherit from Objective-C classes or other @objc classes. They can't be adopted by structures or enumeratoins.

> NOTE: Strictly speaking, you can write a custom class that conforms to CounterDataSource without implementing either protocol requirement. They are both optional, after all. Although technically allowed, this wouldn't make for a very good data source.

**Protocol Extensions**

Protocols can be extended to provide method and property implementations to conforming types. This allows you to define behavior on protocols themselves, rather than in each type's individual conformance or in a global function


























