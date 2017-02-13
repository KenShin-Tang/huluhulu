Swift 中的lexical structure 描述什么样的字符序列组成合法的 tokens of the language(比如 identifier, keyword, punctuation, literal, operator)

### Whitespace and Comments

* Swift中的whitespace的使用是有一定规范的, 大体上有两种方式:
	1. 用来作为源文件中的 tokens间的空白分割;
	2. 用来标识运算符是 prefix 还是 postfix; 
尤其是运算符旁边的whitespace,规则如下:
  1. 如果操作符左右都有whitespace或都没有,则此操作符就是一个二目操作符, 比如 `a+++b`和 `a +++ b`中的 +++ 就被视为二目操作符
  2. 如果操作符只在左边有whitespace, 就被视为前缀单目操作符. 比如`a +++b`中, `+++`就被视为一个前缀单目操作符.
  3.  如果操作符只在右边有whitespace, 就被视为后缀单目操作符. 比如`a+++ b`中, `+++`就被视为一个后缀单目操作符.
  4.  如果操作符左方没有whitespace但后面紧跟一个`.` , 就被视为后缀单目运算符. 比如 `a+++.b`中的 +++

为了遵循上述规则, 在操作符前的`(` `[`和 `{`, 操作符后的`)` `]`和`}` , 以及`,` `:` 和`;` 也都被视为 whitespace.

特别的, 如果`!`和`?` 这两个预定义的操作符在其左边没有whitespace, 就被视为后缀操作符,无视其右是否有whitespace. 使用`?`作为optional-chaning操作符时, 其左边必须没有whitespace. 使用`?`作为条件运算符`?:`中的操作符, 其两侧必须有whitespace.

### Identifiers

除了通常的命名方式, 我们也可以使用 reserved word 进行命名, 为了与这个reserved word 区别开来, 我们可以在其前后加上`` ` ``. 比如`class`是关键字, 我们可以使用`` `class` ``. 其中的反引号`` ` ``并不是这个 identifier 的一部分, 即 `` `x` ``与`x`意义一样.

在没有 explicit parameter names 的 closure 中, 我们可以使用`$0, $1, $2`等来指定第几个参数.

### Keywords and Punctuation


### Literal

A `literal` is the source code representation of a value of a type, such as a number or string.

literal 本身不具有类型属性, 而是被解析为拥有 infinite precision 且 Swift 的类型推断会推测出其类型. 比如, 声明 `let x: Int8 = 42` Swift 会借助类型标注(: Int8)来推断这个 integer literal 的类型为`Int8`. 如果没有足够可用的的信息做推断, Swift 就会将其推断为 Swift 标准库中的一个适当的默认 literal type. 例如integer literal 的 default type 就是`Int`, floting-point literal 的 default type 就是`Double`, string literal 的default type 就是`String`, Boolean literal 的 default type 是`Boolean`. 比如`let str = "Hello, world"`, 默认推断的类型就是`String`.

