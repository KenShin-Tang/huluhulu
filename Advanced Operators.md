####Advanced Operators

Swift中的算数运算符默认是不会溢出的,如果溢出就作为错误来处理.  如果允许溢出行为, 我们在运算符前加 `&`符号.

**Bitwise Operators**

**复合赋值运算符**

> 默认的赋值运算符`=`不能重载; 只有复合运算符才能重载; 类似地, 三目条件运算符`a ? b : c`不能被重载.

**等于运算符**

自定义 classes 和 structures 没有默认的等号/不等号运算符的实现. 因为没有预先定义什么情况下两个实例相等.

