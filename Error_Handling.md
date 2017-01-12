以下两种写法是一致的:
```Swift
//If someThrowingFunction() throws an error, the value of x is nil. Otherwise, the value of x is the value that the function returned. 
let x = try? someThrowingFunction()
和
let x: Int?
do {
  x = try someThrowingFunction()
} catch {
  x = nil
}
```

** Specifying Cleanup Actions**

    You use a `defer` statement to execute a set of statements just before code execution leaves the current block of code. This statement lets you do any necessary cleanup that should performed regardless of how execution leaves the current block of code-- whether it leaves  because an error was thrown or because of a statement such as `return` or `break`.