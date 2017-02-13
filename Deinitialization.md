####Deinitialization

`deinitializer` 在对象(对, 这个只有 class 才有)被销毁前调用.is called immediately before a class instance is deallocted. You write deinitializers with the `deinitializer` keyword, similiar to how initializers are written with the `init` keyword. Deinitializers are only available on class types.

Class definitions can have at most one deinitializer per class. The deinitializer does not take any parameters and is written without parenthese:
```Swift
deinit {
  // perform the deinitialization
}
```
> You are not allowed to call a deinitializer yourself.
> A deinitializer can access all properties of the instance it is called on and can modify its behavior based on those properties.

