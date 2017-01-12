* Swift中的whitespace的使用是有一定规范的,尤其是运算符旁边的whitespace: is used to determine whether an operator is used as a prefix operator, a postfix operator, or a binary operator.规则如下:
  1. 如果操作符左右都有whitespace或都没有,则此操作符就是一个二目操作符, 比如 `a+++b`和 `a +++ b`中的 +++ 就被视为二目操作符
  2. 如果操作符只在左边有whitespace, 就被视为前缀单目操作符. 比如`a +++b`中, `+++`就被视为一个前缀单目操作符.
  3.  如果操作符只在右边有whitespace, 就被视为后缀单目操作符. 比如`a+++ b`中, `+++`就被视为一个后缀单目操作符.
  4.  如果操作符左方没有whitespace但后面紧跟一个`.` , 就被视为后缀单目运算符. 比如 `a+++.b`中的 +++

为了遵循上述规则, 在操作符前的`(` `[`和 `{`, 操作符后的`)` `]`和`}` , 以及`,` `:` 和`;` 也都被视为 whitespace.

特别的, 如果`!`和`?` 这两个预定义的操作符在其左边没有whitespace, 就被视为后缀操作符,无视其右是否有whitespace. 使用`?`作为optional-chaning操作符时, 其左边必须没有whitespace. 使用`?`作为条件运算符`?:`中的操作符, 其两侧必须有whitespace.

