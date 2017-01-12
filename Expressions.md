* The self expressoin is an explicit reference to the current type or instance of the type in which it occurs. It has the following forms:
```Swift
self
self.memberName
self[subscript index]
self(initializer arguments)
self.init(initializer argument)
```

* A superclass expression lets a class interact with its superclass. It has one of the following forms:
```Swift
super.memberName //used to access a member of the superclass
super[subscript index] // used to access the superclass's subscript implementation
super.init(initializer arguments) //used to access an initializer of the superclass
```

**Closure Expression**

```Swift
{ (parameters) -> return type in 
    // statements
}
```
There are several special forms that allow closures to be written more concisely:

* A closure can omit the types of its parameters, its return type, or both. If you omit the parameter names and both types, omit the `in` keyword before the statements. If the omitted types can't be inferred, a compile-time error is raised.
* A closure may omit names for its parameters. Its parameters are then implicitly named $ followed by their position: $0, $1, and so on.
* A closure that consists of only a single expression is understood to return the value of that expression. The contents of this expression are also considered when performing type inference on the surrounding expression.

**Capture lists**

A capture list is written as a comma separated list of expressions surrounded by square brackets, before the list of parameters. If you use a capture list, you must also use the `in` keyword, even if you omit the parameter names, parameter types, and return types.

The entries in the capture list are initialied when the clousure is creates. 每一个capture list里的entry(相对于closure外部, capture list里的量就是外界进入closure的入口) 都会有一个**常量**初始化为closure外部"周围"同名的常量或变量的值.

**Implicit Member Expression**

语法: `.member name`
```Swift
var x = MyEnumeration.SomeValue
x = .AnotherValue
```

**Parenthesized Expression**

A parenthesized expression consists of a comma-separated list of expressions surrounded by parentheses. Each expression can have an optoinal identifier before it, seperated by a colon(:). 

Use parenthesized expressions to create tuples and to pass arguments to a function call. If there is only one value inside the parenthesized expression, the type of the parenthesized expression is the type of that value.

**Wildcard Expression**

A wildcard expression is used to explicitly ignore a value during an asssignment.
```Swift
(x, _) = (10, 20)
```

**Selector Expression**

A selector expression lets you access the selector used to refer to a method in Objective-C.

`#selector(method name)`

the method name must be refrence to a method that is avaliable in the Objective-C runtime.

```Swift
class SomeClass: NSObject {
  @object(doSomethingWithInt:)
  func doSomething(x: Int) {}
}
let x = SomeClass()
let selector = #selector(x.doSomething(_:))
//the method name can contain parentheses for grouping, as well the as operator to disambiguate between methods that share a name but have different type signatures.
```

**Postfix Expression**


**Initializer Expression**

`expression.init(initializer arguments)`

If you specify a type by name, you can access the type's initializer without using an initializer expression. In all other cases, you must use an initializer expression.

**Explicit Member Expression**

我们使用点语法来访问 members of a named type/ a tuple/ a module. 
`expression.member name`



**Postfix Self Expression**

```Swift
expression.self
type.self
```
The first from evaluates to the value of the expression. For example, x.self evaluates to x.

The second from evaluates to the value of the type. Use this form to access a type as a value.


















