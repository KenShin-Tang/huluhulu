#Closures

闭包(Closure)可以捕获其且存储所在上下文的任何常量或者变量的references(看起来就好像将这些常量和变量包裹住了一样)

Closure 有三种形式:
  
* Global functions are closures that have a name and do not capture any values.

* Nested functions are closures that have a name and can capture values from their enclosing function.

* Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.

* Swift中closure的表达是简洁,清晰且鼓励在常见场景中使用语法糖;

 1. 利用上下文推断参数和返回值类型

 2. 隐式返回单表达式闭包,即单表达式闭包可以省略return关键字;

 3. 参数名称简写;

 4. Trailing closure syntax.

* Closure Expressions:

 1. 闭包表达式一般如下:

 ```Swift

 {(parameters) -> returnType in

 	statements

 }

 闭包函数体部分由关键字`in`引入,该关键字表示闭包的参数和返回值类型定义已经完成, 闭包函数体即将开始. parameters 可以是`inout` 修饰的(记住`inout` 修饰的是不能有默认值的).

 ```

 闭包表达式可以使用cons, var和inout类型作为参数,不能提供默认值(注意函数非inout修饰参数是可以设置默认值的).也可以在参数列表的最后使用可变参数.元组也可以作为参数和返回值.



* 单表达式闭包可以通过省略return关键字来隐式返回单表达式的结果. 比如: `reversedNames = names.sorted(by: {s1, s2 in s1 > s2 })`

* Swift自动为内联闭包提供了参数名称缩写功能, 您可以直接通过$0, $1, $2来顺序调用闭包的参数,这样`in`关键字也同样可以被省略.

* 运算符函数(Operator Functions): Swift内建对一些运算符进行了函数实现,因此运算符本身可以作为一个函数来使用.

* Trailing Closures:将一个很长的闭包表达式作为最后一个参数传递给函数, 可以使用Trailing Closure来增加函数的可读性, 比如:

 ```Swift

 func someFunctionThatTakesAClosure(closure:() -> Void) {

 //函数体部分

 }

 //以下是不使用Trailing Closure进行的函数调用

 someFunctionThatTakesAClosure({

 //闭包主体部分

 })

 //以下是使用Trailing Closure进行函数调用

 someFunctionThatTakesAClosure(){

 //闭包主体部分

 }

 ```
 
* 如果函数或者方法本身只有一个参数且为 closure, 我们就可以使用` trailingClosure` 语法来写, 可以省略函数/方法名后的括号`()`.

* Capturing Values: 闭包可以在其被定义的context中捕获cons或者var, 然后就可以在其 body 内部引用/修改这些 constants 和 variables 的值( constants 值不能修改哦), 即便是之前这些值的作用域已不存在. 

``` Swift

	func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}

// incrementer() 函数捕获了 runningTotal 和 amount 并在其自己的 body 使用. 通过reference 捕获 runningTotal 和 amount 保证了它们在 makeIncrementer() 调用后不会被"释放", 而且同时也保证了下次 incrementer() 函数调用时 runningTotal 依然可用.
	
``` 
* 如果被捕获的值 closure 不做修改, 那么(作为优化)就会` copy` 一份存储起来使用.

* Closures本身是引用类型( reference type). whenever you assign a function or a closure to a constant or a variable, you are actually setting that constant or variable to be a `reference` to the function or closure.

* 一个 escaping 修饰的 closure作为一个 function 的参数, 可以"逃出"它所在的函数. 这种情况下, 在关联到`self` 的情况下, 我们就必须显式地指明 self.

```Swift
var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}

func someFunctionWithNoneEscapingClosure(closure: () -> Void) {
    closure()
}
class SomeClass {
    var x = 10
    func doSomethig() {
        someFunctionWithEscapingClosure {
            self.x = 100
        }
        someFunctionWithNoneEscapingClosure {
            x = 200
        }
    }
}
```




* Autoclosures: An `autoclosure` is a closure that is automatically created to wrap an expression that's being passed as an argument to a function. It does'n take any arguments, and when it's called, it return the value of the expressoin that's wrapped inside of it. 过多使用可能使得代码晦涩难懂.



####Classes and Structures



Calsses and Structures are general-purpose, flexible constructs that become the buildig blocks of your program's code.



Swift does not require you to create separate inserface and implementation files for custom classes and structures. In Swift, you define a class or a structure in a single file, and the external interface to that class or structure is automatically made avaliable for other code to use.



Swift classes and structures are much closer in functionality than in other languages.



Classes and Structures in Swift have many things in common.

* Define properties to store values

* Define methods to provide functionality

* Define subscripts to provide access to their values using subscript syntax

* Define initializers to set up their initial state

* Be extended to expand their functionality beyond a default implementation

* Conform to protocols to provide standard functionality of a certain kind



Classes have additional capabilities that structures do not:

* Inheritance enables one class to inherit the charactieristics of another.

* Type casting enables you to check and interpret the type of class instance at runtime

* Deinitializers enable an instance of a class to free up any resources it has assigned.

* Reference counting allows more than one reference to a class instance.



**NOTE:** Structures are always copied when they are passed around in your code, and do not use reference counting.



Definition Syntax:

```Swift

class SomeClass {

 //class definition goes here

 }

struct SomeStructure {

 // structure definition goes here

 }

 ```



Class and Structure Instances:

```Swift

let someResolution = Resolution()

let someVideoMode = VideoMode()

```



Accessing Properties



You can access the properties of an instance using dot syntax. In dot Syntax, you write the property anme immediately after the instance name, separated by a period(.), without any spaces:

```Swift

print("The width of someResolution is \(someResolution.width)")

```

we can drill down into sub-properties, such as the width property in the resolution property of a VideoMode:

```Swift

print("The width of someVideoMode is \(someVideoMode.resolution.width)")

```



* All structures

