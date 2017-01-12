####Subcsipts

Classes, structures, and enumerations can define`subscripts`, which are shortcuts for accessing the member elements of a collection, list, or sequence. You use subscripts to set and retrieve values by index without needing separate methods for setting and retrieval.

**Subscript Syntax**

Subsripts enable you to query instances of a type by writing one or more vlaues in square brackets after the instance name. Their syntax is similar to both instance method syntax and computed property syntax. You write subscript definitions with the `subscript` keyword, and specify one or more input parameters and a return type, in the same way as instance methods. Unlike instance methods, subscripts can be read-write or read-only. This behavior is communicated by a getter and setter in the same way as for computed properties.

**Subscript Usage**

Susscripts are typically used as a shortcut for accessing the member elements in a collection, list, or sequence.

**Subscipt Options**

Subscripts can take any number of input parameters, and these input parameters can be of any type. Subscripts can also return any type. Subscripts can use variable parameters and variadic parameters, but cannot use in-out parameters or provide default parameter values.

