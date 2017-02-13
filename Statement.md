在Swift中有三种statements: simple Statement, compiler control statement 和 control flow statement.

* Simle statements are the most common and consist of either an expression or a declaration. 
* Compiler control statements allow the program to change aspects of the compiler's behavior and include a build configuration  an line control statement.
* Control flow statements are use to control the flow of execution in a program. There are several types of control flow statements in Swift, including loop statement, branch statements, and control transfer statements. 
* Swift中有三种loop statements: for-in, while, repeat-while.
* control flow有: break 和 continue.
* Swift中的repeat-while 可以理解为Objective-C中的do-while
* Swift中有三种branch statements: if ,  guard,   switch;
* 其中guard: A guard statement is used to transfer program control out of a scope if one or more conditions aren't met:
```Swift //其中condition必须遵从BooleanType protocol
guard condition else {
  //statement
  }
  ```
* Swift的switch不会"贯穿"执行: 即其中一个case执行完后,就会exit.
* Labeled statement: 
* Swift有两种compiler control statements: a build configuration statement and a line control statement:
* build configuration:
```Swift
#if build configuration1
  //statements to compile if build configuration 1 is true
#elseif build configuration2
  //statements to compile if build configuration 2 is true
#else
  //statements to compile if both configurations are false
#endif
```
* Line Control Statement: A line cotrol statement is used to specify a line number and filename that can be different from the line number and filename of the source code being compiled.

* Avaliability Condition: An avaliability condition is used as a condition of an if, while, and guard statement to query the availablility of APIs at runtime, based on specified platforms arguments.

An availability condition has the following form:
```Swift
if #available (platform name version, ..., *) {
  //statements to execute if the APIs are available
  } else {
  //fallback statements to execute if the APIs are unavailable
  }
```
























