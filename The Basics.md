### Tuple 数据类型和 optional 类型

Tuples enable you to create and pass around groupings of values. You can use a tuple to return multiple values from a function as a single compound value.

Swift also introduces optional types, which handle the absence of a value. Optioals say either "there is a value, and it equals x" or "there isn't a value at all". Using optionals is similar to using `nil` with pointers in Objective-C, but they work for any type, not just classes.


### Constants and Variables

使用前先声明. `let` 声明 constants. `var` 声明 variables.


####注释

Swift的注释方式有两种: //This is a singleLine comment 和 /* This is a multiLine comment */, 与C中的多行注释不同的是 Swift中的多行注释可以嵌套.

### 打印
默认的打印函数是 `func print(_: Any..., seperator: String, terminator: String` , 它是一个全局函数. 其中` seperator` 是指定打印的值之间的分隔符, `terminator` 是指定换行符.


####分号

Swift不要求你在代码中的每一句声明后都写一个分号(;),当然如果你喜欢,写上也不为过. 但是如果在单行要写多个独立的声明,分号是**不可少**的.



####整数

Swift支持8, 16, 32, 64bit的有符和无符整数. 这些整数命名遵循的惯例与C相似, 如 无符号8bit的整数类型为:UInt8,有符号32bit的整数类型为:Int32. Swift中类型的命名方式都以首字母大写.



####整型数据的边界值或范围(Integer Bounds)

我们可以通过`min`和`max`属性来访问整型类型的最小和最大值:如

```Swift

let minValue = UInt8.min //minValue is equal to 0, and is of type UInt8

let maxValue = UInt8.max //maxValue is equal to 255, and is of type UInt8

```

####Int

大多数情况下,我们无需指明使用特定大小的整型. Swift 提供了一个额外的整数类型, Int(与当前平台的native word size一致),比如在32-bit平台上Int与Int32的size一致, 而64-bit则Int与Int64的size一致.



####UInt

与Int同理.

####浮点型数字(Floating-Point Numbers)

Swift提供了两种有符号的浮点数据类型:

* Double类型表示64-bit的浮点数(至少小数点后15个精度).

* Float 类型表示32-bit的浮点数(可以到小数点后6个精度).



####类型安全与类型推断

Swift是类型安全的. 类型安全的语言会让你清楚地知道你所使用的数据的类型. 如果你代码需要一个String类型,你就不能传个Int.



由于Swift是类型安全的, 所以它就会在编译的时候进行 `type checks`并且会把任何类型不符的标记为错误.这样就能尽可能提前发现错误.



Type-checking 会帮你在使用不同类型时避免错误. 这并不意味着你必须对每一个常量或变量明确声明类型. 不声明时, Swift会使用 `type inference`来推断出类型. 类型推断使得编译器字在编译代码的时候根据你的expression来自动推断出类型(其实就是检测相应的value).



得益于类型推断, Swift相比于C或者Objective-C来说,在类型声明方面大大简化. 常量和变量依然是显式类型的, 只是编译器帮你做了类型声明的工作.



在声明并初始化常量或者变量的时候,类型推断就用处很大了. 就在你给它们赋一个字面量值(literal value)的时候, 类型已经推断出来了.



####数字字面量(Numeric Literals)

在Swift中,我们可以这样书写整数字面量:

* 十进制就是直接书写;

* 二进制数字前面加个 `0b`前缀;

* 八进制数字前面加个 `0o`前缀;

* 十六进制数字前加个 `0x`前缀.



小数字面量:

* 十进制直接书写(也可以使用科学计数法,以e为标示)

* 十六进制除需要 `0x`前缀外,必须使用科学计数法,以p标示)



二者的小数点两侧都必须有数字.

如:



1.25e2 means 1.125 * 10<sup>2<sup>



0xFp2 means 15 * 2<sup>2<sup>



####数字类型转换



即使代码中要用到的数字常量与变量非负, 也请使用Int类型. 日常使用默认整型可以是你的代码可以直接复用并且符合类型推断.



除非特别需要, 才去使用特定类型的整型,比如外部代码明确特定长度的数据类型, 优化性能, 内存使用等. 使用特定长度的类型可以即使捕捉溢出并且明确正在使用的类型.



#### 整型转换

不同长度的整型数据能容纳的数字范围也是不同的,所以如果当前的数值超出类其类型能够容纳的范围,编译会报错.



Swift中没有隐式类型转换, 所以我们通常在将一种类型(显式地)转换为另一种类型的时候. 其实将类型1转换为类型2的背后的机制是: 类型2提供了一个初始化方法接收类型为 类型1的值然后new了一个类型2的实例.



####整型与浮点型数据的转换.

整型与浮点型数据间的转换必须是显式的.



####类型别名(Type Aliases)

`Type aliases` 给现存的类型定一个别名. 使用关键字`typealias`



类型别名在给现有类起一个有"上下文"意义的别名很有用.



####布尔型(Booleans)

Swift有一个基本的布尔类型,叫做`Bool`. 布尔值是用来指定逻辑值的(真或假). 所以Swift内置了两个**布尔常量**,`true`和`false`.

``` Swift

let orangeAreOrange = true

let turnipsAreDelicious = false

```

Swift类型安全会防止非布尔型值替代Bool值.

Swift uses only simple Boolean values in conditional contexts to help avoid

accidental programming errors and to help maintain the clarity of each

control statement. Unlike other programming languages, in Swift integers and strings cannot be used where a Boolean value is expected.



####元组(Tuples)

元组可以将多值(任意类型)打包到一个复合值中. 可以根据 index 来访问某一个元素. Tuples are useful for temporary groups of related values. They are not suited to the creation of complex data structure, rather than as a tuple.



####可选类型(Optionals)

Optionals可以用在值可能确实的情况下: Optional表明一个未知的值或者根本没有值.我们可以近似理解为Objective-C中的nil, 但是nil只能指代objects,而不能指代structure, C基本类型,或枚举类型,这些情况OC中只能通过NSNotFound来指代. 这种方式是假定method的调用者知道要对其进行检测. 而Swift的optionals允许你使用它来指定任何类型为缺失值.



####nil

我们可以使用nil 将optional类型的值置为无值状态.

```Swift

var serverResponseCode: Int? = 404

serverResponseCode = nil

```



**注意*:** nil不能用于非optional 常量或者变量上. 如果你代码中的常量或者变量可能存在值缺失, 最好声明其为optional修饰的类型.



optional variable会默认初始化为nil(除非你初始化赋值).



要注意Swift中的nil与Objective-C中的nil是不同的. 在Objective-C中, nil表示一个指向不存在的对象的指针. 而在Swift中, nil并不是一个指针, 它表示特定类型的值的缺失. Optionals的任何类型均可以设置为nil, 而不仅仅是object.



#### If声明

使用if声明可以检测一个optional修饰的量是否有值(方法就是与nil比较):

```Swift

if convetedNumber != nil {

 print("convertedNumber contains some integer value.")

 }

```

当确认一个optional修饰的量有值, 那么我们就可以在其名字后面添加(!)来访问其值. 这种写法表明" 我知道它是有值的; 尽管使用它." 我们称之为对optional值的`(解包)forced unwrapping`



#可选绑定(Optional Binding) 即 `if/while let constantName = someOptional {}`

我们使用`optional binding`来确认一个optional修饰的量是否有值,如果有, 那么它就可以做为一个临时常量或者变量. `Optional binding` 在if和while声明中来check一个optional修饰的量是否有值, 并且将其解包成一个常量或变量. 比如:

```Swift

if let constantName = someOptional {

 statements//如果someOptional有值,那么就会赋值给constantName,然后我们就可以在if作用域内使用了,即optional的值binding给了constantName

 }

```



常量和变量都可以使用`optional binding`.



甚至你还可以在单个if声明中包含多个`optional binding`,然后使用where分句来check Boolean condition. 如果在这些`optional bindings`中值为nil或者where 分句表达式的值为 false, 整个`optional binding`就会被视为 false.



**Note** 在if声明里进行 `optional binding`的常量或者变量只能在if的作用域内使用. 而在`guard`声明语句中, 常量或者变量 are available in the lines of code that follow the `guard` statement.



#### Implicitly Unwrapped Optionals

如前所述, optionals修饰 表明constant或者variable **可以**没有值. 我们可以通过if声明来检测optional修饰的量是否有值, 如果存在,就可以使用 `optional binding`解包来访问optional修饰量的值.



有时, 我们很清楚程序中的optional修饰的量在首次赋值之后是有值的. 在这种情况下, 我们访问它的时候就可以移除解包操作, 因为这时候是可以确定它是有值的.



这种optional修饰的量就称为`implicitly unwrapped optionals` 我们可以这么书写: 直接在其name后加 `!` 即可,如 `String!` 而不是 `String?` .



什么时候用呢?


The primary use of implicitly unwrapped optionals in Swift is during class initialization. 但是它依然是 optional 的.





####Error Handling

`error handling`可以让你检测到错误的潜在原因,并且将错误传递到你程序的另一块(来做处理).


func canThrowAnError() throws {
    // this function may or may not throw an error
}


当函数触发了错误条件, 它就会`throw`一个error. 该函数的caller就能 `catch`到这个error并且做出合适的响应.



函数在其声明中使用`throw`关键字来表明其能够捕捉error, 你需要在要检测的表达式前添加`try`关键字.

```Swift

do {

 try canThrowAnError()

 //When no error was thrown

} catch {

 //an error was thrown

}

```

do 声明会创建一个闭包, 其内可以允许将错误传递出去.

```Swift

func makeASandwich() throws {

 //...

 }

do {

 try makeASandwich()

 eatASandwich()

 } catch Error.OutOfCleanDishes {

 washDishes()

 } catch Error.MissingIngredients (let ingredients) {

 buyGroceries(ingredients)

 }

```

此例子中,如果 no clean dishes are avaliable or any ingredients are missing, makeASandwich()函数会抛出一个error. 所以就将makeASandwich()函数 wrap到`try`表达中,然后将其放入do 声明中, 抛出的error就会被传递到相应的`catch`分句中做相应的处理.



####断言(Assertions)

某些情形下, 当某个特定条件没有满足而代码可以继续执行,很难做到. 这时我们就可以使用`assertion`来终止代码执行同时可以通过调试来找到值缺失或者非法的原因.



####使用Assertions调试

Assertion 可以在运行时判断一个Boolean条件是否为true. 从字面意思来说, 一个assertion 即是 断定(断言)条件为true. 只有为true的时候代码才能continue executing, 否则, 程序结束.



我们在调试程序的时候, 我们就可以使用assertion在运行时assertion被触发来定位到异常状态及信息(assertion允许我们附带一条响应的debug信息.)



我们可以使用标准库中的全局函数assert(_:_:file:line:)来创建一个assert. 当条件不满足,就可以输出响应的信息,如:

```Swift

let age = 3

assert(age >= 0, "A person's age cannot be less than zero") //this cause the assertion to trigger, because age is not >= 0

```

 #### 使用Assertion的情况

 ...



 ####基本运算符



Swift支持大多数标准C的运算符并且提升了基本其中几个的避免常见编码错误的能力. 比如 赋值运算符 (=) 并不返回值, 这样就防止我们将 = 与 == 搞混用了. 算数运算符能够检测到并且防止值溢出. 与C不同, Swift中的 % 运算符能够计算小数. 并且Swift还提供了两种取数字区间的运算符..<(左闭右开)和...(闭区间).



在Swift中, 赋值运算符两侧要对齐(即a=b 或 a = b, 而不能是a =b). 与C和Objective-C不同的是, Swift的算数运算符不允许值溢出.



#### The Remainder Operator (%)

对整型与浮点型都可使用.

a = (b * multiplier) + remainder (where multiplier is the largest number of multiples of b that will fit inside a)



* 单目运算符 - 与其操作数之间不能有空格(与C和Objective-C不同)

* 单目运算符 + 不改变其操作数的值.(与C和Objective-C一致)

* 复合赋值运算符 +=等等... 同样复合赋值运算符也没有返回值.(同样赋值运算符也没有返回值)

* Swift提供了两个鉴定运算符 ===和!==, 用来检测两个对象的引用的是或否是同一个对象实例.

* 双目或三目运算符中, 操作数与运算符之间加空格.

* Tuple比较时按照顺序比较(Swift标准库中的比较运算符所能比较的元组的元素最多6个), 但是包含 Bool 类型的 tuple 不能做比较运算.

* Nil coalesciing Operator: `??` 比如 a ?? b,如果a有值,则将a解包, 如果a为nil, 则返回b. 其与 a != nil ? a! : b 等价. 主要作用于 optional 类型的值.

* 区间运算符 包括(...闭区间运算符 和 ..<左闭右开区间运算符).

* Swift 中 赋值运算符本身并不返回值(这点与 C 不同) 如 if x=y { // This is not valid, because x = y does not return a value.}







## Strings和 Characters



与Objective-C与Cocoa中的String不同的是, Swift中的String可变与不可变用 变量与常量来区分.



Swift中的String是一个 `value type`, 意味着当你创建一个string然后传递给一个function method 或者赋值给一个变量或者常量的时候, 是`值传递`,即是一份原始值的copy. 这样做更容易控制和安全.(当然Swift编译器是对此做了优化的)

Swift中的 `String` 和 `Character` 类型是 Unicode编码的. 

#### Woking with Characters



**注意:** Extended grapheme clusters由于可以由一个或多个Unicode scalar组成, 所以不同的charaters以及同样的character(如ẻ可以由 \u{65}\u{301}组合而成也可以直接的\u{E9}) 所需要的内存空间也是不同的, 所以string中的characters的numer就无法通过遍历string(因为有extended grapheme cluster).



#### Accessing and Modifying a String

You access and modify a string through its methods and properties, or by subscript syntax.


* Swift strings cannot be indexed by integet values.



Two String values(or two Character values) are considered equal if their extended grapheme clusters are canonically equivalent. Entended grapheme clusters are canonically equivalent if they have the same linguistic meaning and appearance, even if they are composed from different Unicode scalars behind the scenes.



**String and character comparisons in Swift are not locale-sensitive**



#### Swift中的Collection



Swift中内置三种collection:array, set, dictionary.三者都是在generic collection基础上构建的.

* Swift 中 collection 可变的就用 var 声明, let 就是不可变的.

* Array 装载同类型的有序值.

* Set 装载同类型的唯一无序值. 而且 set 中的值类型必须是`hashable`的.(Swift 中的所有基本类型比如String, Int, Double, Bool默认都是 hashable 的)

* 



* Swift的所有基本类型(比如String, Int, Double和Bool)默认都是可哈希化的, 可以所以集合的值的类型或者字典的键的类型.





#### Control Flow



Swift的控制流为: while(重复执行task); if, guard, switch (条件分支task); break, continue(跳转). Swift也提供了for-in循环来遍历 arrays, dictionaries, ranges, strings 以及一些其他的sequences.



Swift中的switch声明也比C中的要强大. 因为Swift中的switch声明不会流转到下一个case, 这样就避免了C中忘记写break声明的错误. 并且case可以是多种不同的匹配模式,比如间隔匹配, tuplers以及指定为特定类型. switch中的case可以是常量或者变量(不必一定是数字)并且可以在case体中使用, 复杂的匹配条件可以使用where分句表达.

* A while loop starts by evaluating a single condition. If the condition is `true`, a set of statement is repeated until the condition become `false`.

**贯穿(fallthrough):**

```Swift

在C中, switch会隐式贯穿即:

switch expression {

 case1:

 case2:

 doSomething;

 break;

 case3:

 doSomething;

 break;

你可以case1中什么也不做,也不break,那么就会自动(隐式地)贯穿到下一个case, 而在Swift中不存在隐式贯穿, switch匹配的case分支中的代码执行完毕后, 程序会中指switch语句, 而不会继续执行下一个分支, 即不需要在case中显式地使用break, 这样Swift更安全易用, 也避免了忘记写break语句而产生的错误. 当然Swift的case也可以包含多个pattern, 用逗号把它们分开

```

* 每一个switch声明必须是`exhaustive` 的, 即每一个要检测的值都要"击中" switch 中的 case.

*  Swift 中switch 允许多 cases 存在交集, 如果某一个某个待检测的值匹配到多个 case, 之后第一个匹配到的 case 执行.

* switch 中的 case 必须是"周全的".

* switch 中允许使用 let 值绑定以及 where 附加条件

**区间匹配:**更接近自然语言, 也很好啊.

```Swift

var naturalCount: String

switch approximateCount {

case 0:

 naturalCount = "no"

case 1..<5:

 naturalCount = "a few"

case 5..<12:

 naturalCount = "several"

case 12..<100:

 naturalCount = "dozens of"

case 100..<1000:

 naturalCount = "hundreds of"

default:

 naturalCount = "many"

}

print("There are \(naturalCount) \(countedThings).")

```



Swift允许多个case匹配同一个值. 实际上, 在这个例子中, 点(0, 0)可以匹配所有四个case. 但是,如果存在多个匹配, 那么只会执行第一个被匹配到的case分支. 考虑点(0, 0)会首先匹配case(0, 0), 因此剩下的能够匹配(0, 0)的case分支都会被忽视掉.



case分支的模式允许将匹配的值绑定到一个临时的constant或者variable, 这些cons或者var在该分支里就可以被引用了-- 这种行为被称为 value binding.



**where:** case分支的模式可以使用where语句来判断额外的条件.



**控制转移语句(Control Transfer Statements):**

控制转移语句改变你代码的执行顺序, 通过它可以实现代码的跳转. Swift有五种控制转移语句:

* continue: 结束当前循环重新开始下一个.

* break

* fallthrough: 实现类似 C 的case 贯穿.

* retrun

* throw



**带标签的声明:** 使用标签来标记一个循环体或者switch代码块, 当使用break或者continue时, 带上这个标签, 可以控制该标签代表对象的中断或者执行.



guard与if之间的区别:

if 声明中的值绑定只能用于if作用域中, 而guard声明中的值绑定可以用在guard后面的guard所在的作用域.



###Checking API Avaliability:



Swift内建支持API检测, 即在特定的部署target上API是否可用, 如果不可用,可以检测出来.

```Swift

if #available(plateform_name version, ..., *) {

 statements to execute if the APIs are avaliable

 } else {

 fallback statements to execute if the APIs are unavailable

 }

```







#### Functions



Swift中的functions都是有类型的, 其类型由参数类型和返回类型组成. 所以一旦确认类型,你就可以像使用Swift中的其他类型一样使用函数类型了, 这样就使得将函数作为参数或返回值传递 变得简单. 另外还有一点觉得新颖的是, Swift的函数是可以嵌套的.



* 每个function都有一个name, 用来描述其做了什么.

* 参数位置与传个它的值要对应.

比如

```Swift

func sayHello(personName: String) -> String {

 let greeting = "Hello, " + personName + "!"

 return greeting

 }

```

例子便是一个函数的定义, 使用一个`func`作为关键字. 使用`->`指代返回值的类型.



```Swift

print(sayHello("Anna"))

```

调用print(_:separator:terminator:) 函数打印.



* Swift的Function的parameters和return types values弹性很大. 我们可以定义一个没有参数名的简单function, 也可以定义一个有表意的参数名以及参数可定制的的复杂函数.



* 每一个 function parameter 都有一个`argument label`和一个'parameter name`, 其中` argument label`

```Swift

func someFunction(argument_Label localParameterName: Int) {

 //function body goes here, and can use localParameterName

 // to refer to the argument value for that parameter

}

我们也可以不写argument_Label以"_"代替. 默认地, 

If you do not want to use an extenal name for the second or subsequent parameters of a function, write an underscore(_) instead of an explicit external name for that parameter.

```

我们也可以给函数的参数在其定义中指定默认值.

```Swift

func someFunction(parameterWithDefault: Int = 12) {

 //function body goes here

 // if no arguments are passed to the function call,

 // value of parameterWithDefault is 12

 }

 ```





* Function都是有返回值的, 只是不显式写的实际上是返回了一个Void类型(空tuple).



* 函数的返回值可以被"忽视"(即不做处理).

* Swift的function的多值返回.

* Function的参数默认是cons.



**In-Out Parameters**

In-Out parameters are passed as follows:



1. When the function is called, the value of the argument is copied.

2. In the body of the function, the copy is modified.

3. When the function returns, the copy's value is assigned to the original argument.



This behavior is known as copy-in copy-out or call by value result.



**NOTE:** In-Out parameters cannot have default values, and variadic parameters cannot be marked as inout.



####Closures



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

 闭包函数体部分由关键字`in`引入,该关键字表示闭包的参数和返回值类型定义已经完成, 闭包函数体即将开始.

 ```

 闭包表达式可以使用cons, var和inout类型作为参数,不能提供默认值(注意函数非inout参数是可以设置默认值的).也可以在参数列表的最后使用可变参数.元组也可以作为参数和返回值.



* 单行表达式闭包可以通过省略return关键字来隐式返回单行表达式的结果.

* Swift自动为内联闭包提供了参数名称缩写功能, 您可以直接通过$0, $1, $2来顺序调用闭包的参数,这样`in`关键字也同样可以被省略.

* 运算符函数(Operator Functions): Swift内建对一些运算符进行了函数实现,因此运算符本省可以作为一个函数来使用.

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

* Capturing Values: 闭包可以在其被定义的context中捕获cons或者var.

* Closures Are Reference Types: functions and closures are reference types. Whenever you assign a function or a closure to a constant or avariable, you are actually setting that constant or variable to be a `regerence` to the function or closure.

* A closure is said to escape a function when the closure is passed as an argument to the function, but is called after the function returns.



* Autoclosures: An `autoclosure` is a closure that is auromatically created to wrap an expression that's being passed as an argument to a function. It does'n take any arguments, and when it's called, it return the value of the expressoin that's wrapped inside of it.



####Enumerations



Enumerations in Swift are first-class types in their own right. Each enumeration definition defines a brand new type. Like other types in Swift, their anmes should start with a capital letter. Give enumeration types singular rather than plural names, so that read as self-evident.



You can define Swift enumerations to store associated values of any type, and the value types can be defferent for each case of the enumeratoin if needed. Enumerations similar to these are known as discriminated unions, tagged unions, or variants in other programming languages.





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








































