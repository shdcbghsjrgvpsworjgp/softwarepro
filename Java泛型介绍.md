# Java泛型

## 一、简介
    
泛型是Java 1.5的新特性，泛型的本质是**参数化类型**，也就是说所操作的数据类型被指定为一个参数。这种参数类型可以用在类、接口和方法的创建中，分别称为**泛型类、泛型接口、泛型方法**。Java泛型被引入的好处是安全简单。在Java SE 1.5之前，没有泛型的情况的下，通过对类型Object的引用来实现参数的“任意化”，“任意化”带来的缺点是要做显式的强制类型转换，而这种转换是要求开发者对实际参数类型可以预知的情况下进行的。对于强制类型转换错误的情况，编译器可能不提示错误，在运行的时候才出现异常，这是一个安全隐患。泛型的好处是在编译的时候检查类型安全，并且所有的强制转换都是自动和隐式的，提高代码的重用率。

## 二、使用规则和限制
   
    1、泛型的类型参数只能是类类型（包括自定义类），不能是简单类型。
    
    2、同一种泛型可以对应多个版本（因为参数类型是不确定的），不同版本的泛型类实例是不兼容的。
    
    3、泛型的类型参数可以有多个。
    
    4、泛型的参数类型可以使用extends语句，例如。习惯上成为“有界类型”。
   
    5、泛型的参数类型还可以是通配符类型。
## 三、实现原理：类型擦出

Java的泛型是伪泛型。在编译期间，所有的泛型信息都会被擦除掉。正确理解泛型概念的首要前提是理解类型擦出（type erasure）。Java中的泛型基本上都是在编译器这个层次来实现的。在生成的Java字节码中是不包含泛型中的类型信息的。使用泛型的时候加上的类型参数，会在编译器在编译的时候去掉。这个过程就称为**类型擦除**。如在代码中定义的`List<object>`和`List<String>`等类型，在编译后都会编程List。JVM看到的只是List，而由泛型附加的类型信息对JVM来说是不可见的。Java编译器会在编译时尽可能的发现可能出错的地方，但是仍然无法避免在运行时刻出现类型转换异常的情况。类型擦除也是Java的泛型实现方法与C++模版机制实现方式（后面介绍）之间的重要区别。

## 四、作用

### 1、泛化。
可以用T代表任意类型Java语言中引入泛型是一个较大的功能增强不仅语言、类型系统和编译器有了较大的变化，以支持泛型，而且类库也进行了大翻修，所以许多重要的类，比如集合框架，都已经成为泛型化的了，这带来了很多好处。

### 2、类型安全。
泛型的一个主要目标就是提高Java程序的类型安全，使用泛型可以使编译器知道变量的类型限制，进而可以在更高程度上验证类型假设。如果不用泛型，则必须使用强制类型转换，而强制类型转换不安全，在运行期可能发生`ClassCastException`异常，如果使用泛型，则会在编译期就能发现该错误。

### 3、消除强制类型转换。
泛型可以消除源代码中的许多强制类型转换，这样可以使代码更加可读，并减少出错的机会。

### 4、向后兼容。
支持泛型的Java编译器（例如JDK1.5中的Javac）可以用来编译经过泛型扩充的Java程序（Generics Java程序），但是现有的没有使用泛型扩充的Java程序仍然可以用这些编译器来编译。

## 五、泛型使用

### 1、泛型类和泛型接口

如果定义的一个类或接口有一个或多个类型变量，则可以使用泛型。泛型类型变量由尖括号界定，放在类或接口名的后面，下面定义尖括号中的T称为类型变量。意味着一个变量将被一个类型替代替代类型变量的值将被当作参数或返回类型。对于`List`接口来说，当一个实例被创建以后，T将被当作一个函数的参数下面分别是泛型类、泛型接口的定义：
```Java
public class Gen<T>{    //泛型类
}
    
public interface List<T> extends Collection<T>{ //泛型接口
}
```
### 2、泛型方法

是否拥有泛型方法，与其所在的类是否泛型无关。要定义泛型方法，只需将泛型参数列表置于返回值前。如：
```java
public class ExampleA{
    public<> voidf（Tx）{
        System.out.println（x.getClass（）.get Name（））；
    }
    publiec static void main（String args[ ]）{
    ExampleA ea= new ExampleA（）；
        ea-f（""）；
        ea.f（10）；
        ea.f（a）；
        ea.f（ea）；
    }
}
```
## 六、优点

Java语言中引入泛型是一个较大的功能增强。不仅语言、类型系统和编译器有了较大的变化，以支持泛型，而且类库也进行了很大的改动，许多重要的类，比如集合框架，都已经成为泛型化的了。这带来了很多好处：
    
### 1、类型安全
泛型的主要目标是提高Java程序的类型安全。通过知道使用泛型定义的变量的类型限制，编译器可以在非常高的层次上验证类型假设。没有泛型，这些假设就只存在于系统开发人员的头脑中。
通过在变量声明中捕获这一附加的类型信息，泛型允许编译器实施这些附加的类型约束。类型错误就可以在编译时被捕获了，而不是在运行时当作`ClassCastException`展示出来。将类型检查从运行时挪到编译时有助于Java开发人员更早、更容易地找到错误，并可提高程序的可靠性。

### 2、消除强制类型转换
泛型的一个附带好处是，消除源代码中的许多强制类型转换。这使得代码更加可读，并且减少了出错机会。尽管减少强制类型转换可以提高使用泛型类的代码的累赞程度，但是声明泛型变量时却会带来相应的累赞程度。在简单的程序中使用一次泛型变量不会降低代码累赞程度。但是对于多次使用泛型变量的大型程序来说，则可以累积起来降低累赞程度。所以泛型消除了强制类型转换之后，会使得代码加清晰和筒洁。

### 3、更高的运行效率
在非泛型编程中，将筒单类型作为`Object`传递时会引起`Boxing`（装箱）和`Unboxing`（拆箱）操作，这两个过程都是具有很大开销的。引入泛型后，就不必进行`Boxing`和`Unboxing`操作了，所以运行效率相对较高，特别在对集合操作非常频繁的系统中，这个特点带来的性能提升更加明显。

### 4、潜在的性能收益
泛型为较大的优化带来可能。在泛型的初始实现中，编译器将强制类型转换（没有泛型的话，Java系统开发人员会指定这些强制类型转换）插入生成的字节码中。但是更多类型信息可用于编译器这一事实，为未来版本的JVM的优化带来可能。