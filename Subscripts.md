####Subcsipts

Classes, structures, and enumerations 定义`subscripts`是一种简便访问集合类(比如 collection, list, sequence)成员的方式.can define`subscripts`. 我们可以利用 subscripts 来设置或获取成员的值而无需额外的方法来实现. 比如要访问一个`Array`中的元素, 我们就可以使用`someArray[index]`; 访问` Dictionary` 中的元素, 使用`someDictionary[key]`.

**Subscript Syntax**

Subsripts enable you to query instances of a type by writing one or more vlaues in square brackets after the instance name. Their syntax is similar to both instance method syntax and computed property syntax. You write subscript definitions with the `subscript` keyword, and specify one or more input parameters and a return type, in the same way as instance methods. Unlike instance methods, subscripts can be read-write or read-only. This behavior is communicated by a getter and setter in the same way as for computed properties.

**Subscript Usage**

Susscripts are typically used as a shortcut for accessing the member elements in a collection, list, or sequence.

**Subscipt Options**

Subscripts 可以有任意多个不同类型的参数同时也可以返回任意类型.  Subscripts 可以使用variadic parameters, 但是不能使用 in-out 参数以及有默认值的参数. 就说这么多吧.

