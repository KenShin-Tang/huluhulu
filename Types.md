####Types

In Swift, 可以将type分为两类: named types 和 compound types.
* Named type: 在定义时就拟定一个名字, 我们所熟知的classes, structures, enumerations, and protocols. 比如我们定义了一个名为"MyClass"的类型, 那么它的类型就是`MyClass`. Swift标准库里有很多我们熟悉的类型, 如数组类型, 字典类型, 和 可选值类型(optional values).

在一门语言里数据类型通常是最基本最重要的, 比如代表numbers, characters, 和strings的那些类型, 它们实际上就是`named type`-由Swift标准库来定义和实现的structures. 因为是named types, 所以我们可以使用extention来拓展它以为我所用.

* Compound type: 是Swift定义的一种类型, 它没有名字. 有两种compound types: function types 和 tuple types. 一个compound types可以包含named types以及其他compound types. 比如, tuple类型 `(Int, (Int, Int))`包含两个元素, 一个是named type: `Int`, 另一个是 compound type: `(Int, Int)`.

类型声明语法:
> *type-annotation  -> * `: attributes`<sub>*opt*</sub>  `type`

* 类型ID

类型标识符: refers to either a named type or a type alias of a named or compound type.

通常我们将类型名用作类型标志符来直接指明这种类型. 比如`Int`就是直接指明Int类型的类型标志符. 当然也有类型标志符不是类型本身的name(有可能根本就没name), 比如 tuple type(Int, Int):
```Swift
typealias Point = (Int, Int)
let origin: Point = (0, 0)
```
另一种情况是我们代码引用其他module的named type(这时我们不能直接使用类型的name), 我们使用`.`语法来指明, 比如:
```Swift
var someValue: ExampleModule.MyType
```
类型标志符语法:
> *type-identifier  ->* `type-name generic-argument-clase`<sub>opt</sub> ` | ` `type-name generic-argument-clause`<sub>opt</sub>`. type-identifier` 
> *type-name*  ->  `identifier`

**Function Type**

A function type represents the type of a function, method, or closure and consists of a parameter and return type seperated by an arrow(->):

`parameter type -> return type`

