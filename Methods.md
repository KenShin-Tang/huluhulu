####Methods

方法(method) 就是与特定类型相关联的函数(function).

* Class, structure, enumeration 都可以定义实例方法(`instance methods`) 和 类型方法(`type methods`).

**Instance Methods**

* 可以访问/修改 instance 的 properties或者一些相关的功能.
* instance method 写在它所属的类型中. 可以访问这个type中的所有其他instance methods 和 properties.

**Local and External Parameter Names for Methods**

Function parameters can have both a local name(for use within the function's body) and an externalname(for use when calling the function).

* Swift中方法中的第一个parameter默认的表示为local parameter name, 并且第二个和后续的parameter默认表示both local and external parameter name.

**Modifying External Parameter Name Behavior for Methods**

Sometimes it's useful to provide an external parameter anme for a methods's first parameter, even though this is not the default behavior. To do so, you can add an explicit external name yourself.

If you do not want to probide an external name for the second or subsequent parameter of a method, override the default by using an undersocre character(_) as an explicit external parameter name for that parameter.

**The self Property**

* 每个实例都有一个隐式的 property叫做`self`,即实例本身. 我们可以在实例方法中使用 self 来指代这个实例本身. 

* 我们在实例方法的参数与其类型中的某个属性 名称相同时, 可以使用`self.propertyName`来指代属性. 我们通常可以在方法中省略 self(如果方法参数名与 property name 重复, 那么为了分辨就需要指代 property 时使用 self)

**Modifying Value Types from Within Instance Methods**

Structures and enumeration are value types. By default, the properties of a value type cannot be modified from within its instance methods. (为何, 看这里[为何](http://stackoverflow.com/questions/24035648/swift-and-mutating-struct))

如果确实需要使用类型中的methods来修改structure或者enumeration中的properties, 我们可以使用`mutating func`来修饰func. The `mutating` keyword is added to its definition to enable it to modify its properties.

 *NOTE that you cannot call a mutating method on a constant of structure type, because its properties cannot be channed, even if they are variable properties, as described in Stored Properties of Constant Structure Instances:*
  
****

  **Type Methods**
    
* 类型方法我们使用`static`前缀来加以修饰, 特别的对于Class的类型方法,如果它可以被覆写那么我们特别使用`class`修饰.(*与property很类似啊,其实都是这样的,与类型相关的都用static修饰,特别地与class相关的且可被覆写的使用class修饰*)
* 同样在类型方法中,self指代类型本身, 如果有类型方法参数名与类型本身的property名称一致,我们使用self.property来区分.
  























