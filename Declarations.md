##Declarations

A declaration introduces a new name or construct into your program.

* Top-Level Code: the top-level code in a Swift source file consists of zero or more statements, declarations, and expressions. By default, variables, constants, and other named declarations that are declared at the top-level of a source file are accessible to code in every source file that is part of the same module.

* Rethrowing Functions and Methods

A function or method can be declared with the `rethrows` keyword to indicate that it throws an error only if one of its function parameters throws an error. These functions and methods are known as rethrowing functions and rethrowing methods.

* Enumeration declaration

An enueration declaration introduces a named enumeation type into your program. Enumearation delcarations can't contain deinitializer or protocol declarations. 不能继承;没有默认的initializer; 所有的initializer必须明确声明. enumeration是值类型.

* Protocol Declaration不能包含其他的declarations.

* Declaration Modifiers: Declaration modifiers are keywords or context-sensitive keywords that modify the behavior or meaning of a declaration. 
* `dynamic`: Apply this modifier to any member of a class that can be represented by Objective-C. When you mark a member declaration with the `dynamic` modifier, access to that member is always dynamically dispatched using the Objective-C runtime.
* `final`: Apply this modifier to a class or to a property, method, or subscript member of a class. It's applied to a class to indicate that the class can't be subclassed. It's applied to a property, method, or subscript of a class to indicate that a class member can't be overridden in any subclass.
* `lazy`: Apply this modifier to a stored varialbe property fo a class or structure to indicate that the property's initial value is calculaed and stored at most once, when the property is first accessed.
* `optional`: Apply this modifier to a protocol's property, method, or subscript members to indicate that a conforming type isn't retuqired to implement those members. **You can apply the `optional` modifier only to protocols that are marked with the `objc` attribute. As a result, only class types can adopt and conform to a protocol that contains optional member requirements.**
* `required`: Apply this modifier to a designated or convenience initializer of a class to indicate that every subclass must implement that initializer. The subclass's implementation of that initializer must also be marked with the required modifier.

* `weak`: The `weak` modifier is applied to a variable or a stored variable property to indicate that the variable or property has a weak reference to the object stored as its value. The type of the variable or property must be an optional class type. Use the `weak` modifier to avoid strong reference cycles. 
























