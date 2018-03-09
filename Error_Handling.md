## 异常处理

Swift 中为在运行时抛出, 捕获, 传递, 处理(可处理的)提供了"first-class" 级别的支持.

程序的运行通常不能完全保证执行正常且合理输出. Optionals 可用来代表值可缺失, 但是一旦代码未按正常路径执行而产生错误, 我们要知道哪里出错了, 就必须对异常做出相应的响应.

举个例子, 一个从磁盘上读取文件数据的 task, 有很多可能这个 task 会失败, 比如文件不存在, 没有读取权限, 无法解码等. 在这些不同的情形中区分出不同错误, 能处理的处理, 不能处理的通知用户, 这就是我们 Error Handling 要做的.



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