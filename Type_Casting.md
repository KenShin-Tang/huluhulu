####Type Casting

`Type Casting` is a way to check the type of an instance, or to treat that instance as a different superclass or subclass from somewhere else in its own class hierarchy.

Type casting in Swift is implemented with the `is` and `as` operators.

> NOTE: Casting does not actually modify the instance or change its values. The underlying instance remains the same; it is simply treated and accessed as an instance of the type to which it has been cast.

**Type Casting for Any and AnyObject**

Swift provides two special type aliases for working with non-specific types:

* `AnyObject` can represent an instance of any class type.
* `Any` can represent an instance of any type at all, including function types.

> NOTE: Use `Any` and `Any` only when you explicitly need the behavior and capabilities they provide. It is always better to be specific about the types you expect to work in your code.

