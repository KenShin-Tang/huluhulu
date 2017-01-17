#Enumerations

* Swift 中的`Enumeration` 相比于 C更加灵活, 它的case 的`值(value)`即` raw`value可以是 string, character, 或者 int , float 类型,而不仅仅是 C 中的 int 值, 而且不必每一个 case 都有值.

*  Swift中的 每一个不同的enumeration case值可以关联任意类型的值, 这个很像其他语言中的 `unions`或者`variants`. 我们可以将一系列的关联 cases 定义到一个 set中作为一个 enumeration 的一部分, 每一个 enumeration 都有**一组**恰当类型的值与之关联.

* Enumerations在 Swift 中是first-class types. 所以每一个Enumeration 都是一个全新的 type, 所以类型名首字母大写. Give enumeration types singular rather than plural names, so that read as self-evident.

```Swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}
```

### Associated Values(关联值)

* 有时将 case与相关的类型的值关联起来会很有用. 这样我们就可以使用相应的 case 来存储关联类型的值(信息). 比如如下例子, 我们有一个` Barcode` 的 Enumeration 类型, 它包含两种 case:

```Swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```
上面可以读作: 定义一个叫`Barcode` 的 Enumeration 类型, 它可以取 upc(关联一个(Int, Int, Int, Int)类型) 或者 qrCode(关联一个 String 类型) 两者之一. 它并不会有实际的 Int 或者 String 值, 只是定义了可以被`Barcode`类型的常量或者变量存储的关联值的类型, 以便明确当值为` Barcode.upc` 或者 `Barcode.qrCode` 时,我们可以关联存储的值的类型.

### Raw values(原始值)

* Enumeration 中的 cases 可以预置默认值(类型一致).

```Swift
enum ASCIIControlCharacter: Character {
	case tab = "\t"
	case lineFeed = "\n"
	case carriageReturn = "\r"
}
```
Int 类型的 raw value 默认与 C语言一样, 从0逐个按1递增; String类型的 raw value 默认就是 case's name.

### 递归 Enumeration

使用` indirect` 来修饰 case.


















