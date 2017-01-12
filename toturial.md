* `if` statement 中conditional必须是一个 Boolean expression, 而不能是诸如`if noneBooleanValue {...}`这样的, 即不是向 C 一样的与0的隐式比较结果.

* `if let`可与`optional`类型(要么有值要么就是 nil)的值一块使用来判定 optional 类型(变量类型后面紧跟?来标识, 如`var optionalString: String? = "Hello"`)是否为 `nil`, 即optional类型的量是否"有值".

*