* `if` statement 中conditional必须是一个 Boolean expression, 而不能是诸如`if noneBooleanValue {...}`这样的, 即不是向 C 一样的与0的隐式比较结果.

* `if let`可与`optional`类型(要么有值要么就是 nil)的值一块使用来判定 optional 类型(变量类型后面紧跟?来标识, 如`var optionalString: String? = "Hello"`)是否为 `nil`, 即optional类型的量是否"有值". 其实以下两种写法的效果是一样的:

```Swift
var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
-------------------------------------------
if let name = optionalName {
	greeting = "Hello, \(name)"
}
-------------------------------------------
				 ||
				 ||
				 ||
				\||/
				 \/
if optionalName != nil {
	let a = optionalName!;
	greeting = "Hello, \(a)"
}
```

* optional value 可以有默认值, 写法是在其后面加上```??默认值```, 比如

```
let nickName: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickName ?? fullName)"
```

* By default, functions use their parameter names as labels for their arguments. Write a custom argument label before the parameter name, or write _ to use no argument label.

* 闭包:blocks of code that can be called later. The code in a closure has access to things like variables and functions that were available in the scope where the closure was created, even if the closure is in a different scope when it is executed --  函数本身就是一种特殊的闭包