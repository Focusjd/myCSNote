# JAVA Notes

### String

**Note:** 尽管有string池，但是不能保证编译器的优化，所以**应该使用 .equals()**

String 被声明为 final，因此它不可被继承。

由于字符串（`String`）的不变性（immutability），Java中的字符串行为在某些情况下看起来与基本数据类型（如`int`）相似，尤其是在赋值和参数传递的行为方面。但是，重要的是要理解它们在本质上仍然是不同的：

1. **存储方式**：
   - 基本类型（如`int`）存储的是数据值本身。
   - 引用类型（如`String`）存储的是指向对象内存地址的引用。
2. **不变性与可变性**：
   - 基本类型的值是可变的。你可以改变一个基本类型变量的值，而不会影响其他变量。
   - **`String`是不可变的。任何对字符串的修改都会产生一个新的`String`对象，而不是更改现有对象的内容。**任何看似改变字符串内容的操作(例如拼接)实际上都是创建了一个新的`String`对象，而不是修改原有对象。
3. **参数传递**：
   - 无论是基本类型还是引用类型，Java方法参数的传递都是值传递。对于基本类型，传递的是值的拷贝；对于引用类型，传递的是引用的拷贝。
   - **对于`String`，由于其不变性，即使它是引用类型，方法内对参数的修改（指向新对象）不会影响到原始引用。这种行为在某种程度上与基本类型类似，因为基本类型的值传递也不会影响原始变量。**
4. **性能差异**：
   - 基本类型通常比引用类型更高效，因为它们直接存储值，而不涉及堆内存的分配和垃圾回收。
5. **字符串池**：
   - `String`类型有一个特殊的特性，即字符串池。这是一种优化，使得相同内容的字符串字面量共享同一个实例。这种行为是基本类型没有的。

**因为不可变所以可以有：缓存池，或者string可以用作hashmap的key**



#### Java缓存池

Java的缓存池，通常指的是Java在处理某些类型的数据时，为了提高效率和减少内存使用，而采用的一种机制，这种机制允许重复使用不变的对象。最常见的例子是整数和字符串的缓存池。

1. **字符串常量池（String Pool）**：

   - 当创建字符串时，Java首先检查字符串常量池中是否已存在相同内容的字符串。
   - 如果存在，Java会返回对该字符串的引用，而不是创建一个新对象。
   - 这种方法可以减少内存消耗，并提高性能。
   - 字符串常量池位于Java堆内存中。

2. **整数缓存池（Integer Cache）**：

   **在Java中，`Integer`缓存池的概念仅适用于`Integer`对象，而不适用于基本数据类型`int`。**

   - Java对-128到127之间的整数进行了缓存（这个范围可以通过JVM设置进行调整）。
   - 当创建这个范围内的整数对象时，会从缓存池中获取，而不是每次都创建新的对象。
   - 这样做主要是因为这个范围内的整数使用非常频繁，使用缓存可以提高效率。

3. **除了Float 和Double 之外，其他六个包装器类（Byte、Short、Integer、Long、Character、Boolean）都有常量缓存池**

每次你声明一个新的`int`变量或者给变量赋值，它都会在内存中占用一个新的位置，存储其数值。这是因为`int`是一个基本数据类型，不是对象

### Java的类型提升规则

当表达式中涉及多种不同的数据类型时，**较小的数据类型会被提升到较大的数据类型**，以保持数据的准确性和**避免数据丢失**。例如: ```cha+int+double =double``







### HashMap

1. 同步性
   - `HashMap`是非同步的。这意味着它不是线程安全的，如果多个线程同时访问并修改一个`HashMap`，需要外部同步。
2. 性能
   - 由于非同步，`HashMap`通常比`Hashtable`有更好的性能。
3. Null值
   - `HashMap`允许一个null键和多个null值。
4. 迭代顺序
   - `HashMap`中的元素没有保证的顺序，或者顺序随时间发生变化。
5. 散列和容量
   - `HashMap`提供了调整负载因子和初始容量的选项，以优化存储和性能。

### Hashtable

1. 同步性
   - `Hashtable`是同步的。每个方法都是线程安全的，但这会带来性能开销。
2. 性能
   - 由于其同步性，`Hashtable`在多线程环境中比`HashMap`慢。
3. Null值
   - `Hashtable`不允许键或值为null。
4. 迭代顺序
   - 与`HashMap`类似，`Hashtable`中的元素没有确定的顺序。
5. 遗留类
   - `Hashtable`是Java早期版本的一部分，现在主要出于兼容性原因而存在。

### 使用建议

- 在非多线程环境下，推荐使用`HashMap`，因为它更快。
- 如果需要线程安全的映射，并且可以承受同步带来的性能损失，可以考虑`Hashtable`。但在多数情况下，更好的选择是使用`Collections.synchronizedMap`将`HashMap`包装成线程安全的，或者使用`ConcurrentHashMap`，后者提供了更高的并发性。
- `Hashtable`因为其设计上的限制（如不允许null值）和较老的实现，在新代码中使用较少。



### final

1. 变量：

- **基本数据类型**：变量的值不能改变。
- **引用数据类型**：引用的对象不能改变，但对象本身的状态（它的字段值）可以改变。

2. 方法：

   final 不能被重写

   private 方法隐式地被指定为 final，如果在子类中定义的方法和基类中的一个 private 方法签名相同，此时子类的方法不是重写基类方法，而是在子类中定义了一个新的方法。（`private`方法对其所在类之外是不可见的。这意味着即使子类继承了一个有`private`方法的父类，子类也无法“看到”这个`private`方法。由于子类不能访问、覆盖或以任何方式改变这个`private`方法，因此从实际角度来看，这个方法是final的。）

3. 类：

​	不能被继承





### 类初始化

在Java中，一个类的初始化发生在首次使用时，具体来说，包括以下几种情况：

1. **创建类的实例**： 当首次创建类的实例时，Java虚拟机（JVM）会初始化该类。这包括为类的静态成员变量分配空间并设置初始值，然后执行静态初始化块。
2. **访问类的静态成员**： 当首次访问类的静态成员（变量或方法）时，类将被初始化。这不仅适用于静态变量的读取，也适用于静态方法的调用。
3. **使用类或接口的静态方法**： 当使用类的静态方法时，类将被初始化。
4. **初始化子类**： 如果一个类是另一个类的子类，初始化子类时，会先初始化其父类（除非父类已经被初始化）。
5. **Java虚拟机启动时**： 如果类是一个启动类（即包含 `main` 方法的类），在Java虚拟机启动时，该类会被初始化

### static

存在继承的情况下，初始化顺序为：

- 父类（静态变量、静态语句块）
- 子类（静态变量、静态语句块）
- 父类（实例变量、普通语句块）
- 父类（构造函数）
- 子类（实例变量、普通语句块）
- 子类（构造函数）

静态变量和静态语句块优先于实例变量和普通语句块，静态变量和静态语句块的初始化顺序取决于它们在代码中的顺序。

**1. 静态变量**

- 静态变量：又称为类变量，也就是说这个变量属于类的，类所有的实例都共享静态变量，可以直接通过类名来访问它。静态变量在内存中只存在一份。
- 实例变量：每创建一个实例就会产生一个实例变量，它与该实例同生共死。

**2. 静态方法**

静态方法在类加载的时候就存在了，它不依赖于任何实例。所以静态方法必须有实现，也就是说它不能是抽象方法。静态方法只能访问所属类的静态字段和静态方法，方法中不能有 this 和 super 关键字，因为这两个关键字与具体对象关联。

**3. 静态语句块**

静态语句块在类初始化时运行一次。

**执行顺序**： 如果一个类中有多个静态语句块，它们将按照在类中出现的顺序执行。

**4. 静态内部类**

非静态内部类依赖于外部类的实例，也就是说需要先创建外部类实例，才能用这个实例去创建非静态内部类。而静态内部类不需要。

当 `final` 和 `static` 一起使用时，变量变成了**静态常量**。这意味着它是类级别的（与任何特定实例无关），且一旦被赋值后就不能更改。**且这些字段的访问不会触发类的初始化**





### switch

支持int，Java 7 之后支持String 对象

```java
switch (expression) {
    case value1:
        // 代码块
        break;
    case value2:
        // 代码块
        break;
    ...
    default:
        // 所有其他情况的代码块
}
```



### 多肽Polymorphism

父类引用指向子类对象（类别是父类但行为本身是子类，重写的方法会执行子类，但是只能访问父类有的属性和方法）

```Father a = new Child();```

- **多态**：这是实现多态的一种方式。父类引用可以指向任何一个继承自该父类的子类对象。
- **方法覆盖**：如果**子类重写了父类**的方法，通过父类引用调用该方法时，将**执行子类中的版本**。
- **限制**：虽然父类引用可以指向子类对象，但它**只能访问父类中定义的方法和变量**，不能访问子类中新增的成员。
- **类型转换**：如果需要访问子类特有的成员，可以将父类引用**强制转换**为子类类型（前提是引用确实指向了子类对象）。





### Object通用方法

```java
public native int hashCode()

public boolean equals(Object obj)

protected native Object clone() throws CloneNotSupportedException

public String toString()

public final native Class<?> getClass()

protected void finalize() throws Throwable {}

public final native void notify()

public final native void notifyAll()

public final native void wait(long timeout) throws InterruptedException

public final void wait(long timeout, int nanos) throws InterruptedException

public final void wait() throws InterruptedException
```

#### equals()

- 对于基本类型，== 判断两个值是否相等，基本类型没有 equals() 方法。
- 对于引用类型，== 判断两个变量是否引用同一个对象，而 equals() 判断引用的对象是否等价。



#### hashCode()

hashCode() 返回哈希值，而 equals() 是用来判断两个对象是否等价。等价的两个对象散列值一定相同，但是散列值相同的两个对象不一定等价，这是因为计算哈希值具有随机性，两个值不同的对象可能计算出相同的哈希值。

在覆盖 equals() 方法时应当总是覆盖 hashCode() 方法，保证等价的两个对象哈希值也相等。

HashSet 和 HashMap 等集合类使用了 hashCode() 方法来计算对象应该存储的位置，因此要将对象作为键添加到这些集合类中，需要让对应的类实现 hashCode() 方法。



### java 访问级别

Java中的访问权限是指一个类的成员（变量、方法、构造器等）对其他类的可见性。类只有default和public，且决定了类的成员的最大访问权限。（其他包无法访问具有`default`（默认）访问权限的类，即使该类中有`public`方法也是如此。）

1. **Private（私有）**:
   - **作用范围**：仅在定义它们的类内部可见。
   - **用途**：用于隐藏类的内部实现细节，不希望外部直接访问的成员变量和方法。
2. **Default（默认，又称为Package-Private）**:
   - **作用范围**：同一包内的类可以访问，不使用任何修饰符。
   - **用途**：对于包内部的类来说是可见的，但对于其他包中的类来说是隐藏的。
3. **Protected（受保护的）**:
   - **作用范围**：同一包内的其他类以及不同包中的子类可以访问。
   - **用途**：通常用于允许类的子类访问父类的成员，同时对其他类隐藏。
4. **Public（公共的）**:
   - **作用范围**：对所有类可见。
   - **用途**：通常用于定义API的公共接口部分，使得任何外部类都可以使用这些公共成员。

`default`访问级别限制访问范围在同一包内，而`protected`访问级别扩展了这一范围，包括同一包内的类和所有子类（即使这些子类在不同的包中）。



### 抽象类和接口 abstract class and interface

- **抽象类**：通常用于表示“是一个”关系，表示一个更具体的事物。
- **接口**：通常表示“能做什么”或“有什么功能”。

1. **方法实现**:
   - **抽象类**：可以包含具体实现的方法（包括构造器）和抽象方法（没有具体实现的方法）。
   - **接口**：在Java 8之前，接口只能包含抽象方法（没有具体实现）。从Java 8开始，接口也可以包含默认（default）和静态（static）方法，它们有具体实现。这是因为不支持默认方法的接口的维护成本太高了。在 Java 8 之前，如果一个接口想要添加新的方法，那么要修改所有实现了该接口的类，让它们都实现新增的方法。
2. **继承和实现**:
   - **抽象类**：一个类只能继承一个抽象类。
   - **接口**：一个类可以实现多个接口。
3. **构造器**:
   - **抽象类**：可以有构造器。
   - **接口**：不能有构造器。
4. **成员变量**:
   - **抽象类**：可以包含各种类型的变量（比如`private`, `protected`, `public`）。
   - **接口**：所有的成员变量默认都是`public static final`的，也就是说它们是**常量**。
5. **访问修饰符**:
   - **抽象类**：成员可以有不同的访问修饰符（`private`, `protected`, `public`）。
   - **接口**：在Java 9之前，接口的方法默认是`public`的。Java 9引入了私有方法，允许在接口中定义私有方法和私有静态方法。
6. **使用场景**:
   - **抽象类**：当多个类之间存在较高的共享代码时使用，或者需要继承非静态和非常量字段。
   - **接口**：用于定义不同类之间共享的公共行为，特别是当这些类可能属于不同的类层次结构时。
7. **实例化**:
   - **抽象类和接口**：都不能被实例化。

**例子：**

使用接口：

- 需要让不相关的类都实现一个方法，例如不相关的类都可以实现 Comparable 接口中的 compareTo() 方法；
- 需要使用多重继承。

使用抽象类：

- 需要在几个相关的类中共享代码。
- 需要能控制继承来的成员的访问权限，而不是都为 public。
- 需要继承非静态和非常量字段。



### Super

##### 1. 引用父类的属性和方法

当子类覆盖（Override）了继承自父类的方法或属性时，可以使用 `super` 关键字来引用父类的版本。

```java
class Parent {
    void display() {
        System.out.println("Display method in Parent");
    }
}

class Child extends Parent {
    void display() {
        super.display();  // 调用父类的display方法
        System.out.println("Display method in Child");
    }
}
```

##### 2. 调用父类的构造函数

`super` 也用于子类构造函数中，以调用父类的构造函数。这是初始化子类对象时，确保父类成员被适当初始化的一种方式。

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
public class Student extends Person {
    private String studentId;

    public Student(String name, int age, String studentId) {
        super(name, age);  // 调用父类的构造函数
        this.studentId = studentId;
    }
}
```

- **`super()` 调用必须是子类构造函数中的第一个语句。**
- **如果父类没有无参构造函数，子类的构造函数必须显式调用 `super()` 并提供必要的参数**，否则编译器会报错。
- 如果父类有一个无参构造函数，那么子类在不显式调用 `super()` 的情况下，编译器会自动调用父类的无参构造函数。



### 重写与重载

**1. 重写（Override）**

存在于继承体系中，指子类实现了一个与父类在方法声明上完全相同的一个方法。

为了满足里式替换原则，重写有以下三个限制：

- 子类方法的访问权限必须大于等于父类方法；
- 子类方法的返回类型必须是父类方法返回类型或为其子类型。
- 子类方法抛出的异常类型必须是父类抛出异常类型或为其子类型。

使用 @Override 注解，可以让编译器帮忙检查是否满足上面的三个限制条件。

下面的示例中，SubClass 为 SuperClass 的子类，SubClass 重写了 SuperClass 的 func() 方法。其中：

- 子类方法访问权限为 public，大于父类的 protected。
- 子类的返回类型为 ArrayList<Integer>，是父类返回类型 List<Integer> 的子类。
- 子类抛出的异常类型为 Exception，是父类抛出异常 Throwable 的子类。
- 子类重写方法使用 **@Override** 注解，从而让编译器自动检查是否满足限制条件。

```java
class SuperClass {
    protected List<Integer> func() throws Throwable {
        return new ArrayList<>();
    }
}

class SubClass extends SuperClass {
    @Override
    public ArrayList<Integer> func() throws Exception {
        return new ArrayList<>();
    }
}
```



在调用一个方法时，先从本类中查找看是否有对应的方法，如果没有再到父类中查看，看是否从父类继承来。否则就要对参数进行转型，转成父类之后看是否有对应的方法。总的来说，方法调用的优先级为：

- this.func(this)
- super.func(this)
- this.func(super)
- super.func(super)



**2. 重载（Overload）**

方法重载发生在单个类中或子类中，指一个方法与已经存在的方法名称上相同，但是参数类型、个数、顺序至少有一个不同。应该注意的是，返回值不同，其它都相同不算是重载（返回类型必须相同或符合协变返回类型的规则）。



### 反射

参考链接: https://www.liaoxuefeng.com/wiki/1252599548343744/1255945147512512

每个类都有一个 **Class** 对象，包含了与类有关的信息。当编译一个新类时，会产生一个同名的 .class 文件，该文件内容保存着 Class 对象。

类加载相当于 Class 对象的加载，类在第一次使用时才动态加载到 JVM 中。也可以使用 `Class.forName("com.mysql.jdbc.Driver")` 这种方式来控制类的加载，该方法会返回一个 Class 对象。

反射可以提供运行时的类信息，并且这个类可以在运行时才加载进来，甚至在编译时期该类的 .class 不存在也可以加载进来。

Class 和 java.lang.reflect 一起对反射提供了支持，java.lang.reflect 类库主要包含了以下三个类：

- **Field** ：可以使用 get() 和 set() 方法读取和修改 Field 对象关联的字段；
- **Method** ：可以使用 invoke() 方法调用与 Method 对象关联的方法；
- **Constructor** ：可以用 Constructor 的 newInstance() 创建新的对象。

**反射的优点：**

- **可扩展性** ：应用程序可以利用全限定名创建可扩展对象的实例，来使用来自外部的用户自定义类。
- **类浏览器和可视化开发环境** ：一个类浏览器需要可以枚举类的成员。可视化开发环境（如 IDE）可以从利用反射中可用的类型信息中受益，以帮助程序员编写正确的代码。
- **调试器和测试工具** ： 调试器需要能够检查一个类里的私有成员。测试工具可以利用反射来自动地调用类里定义的可被发现的 API 定义，以确保一组测试中有较高的代码覆盖率。

**反射的缺点：**

尽管反射非常强大，但也不能滥用。如果一个功能可以不用反射完成，那么最好就不用。在我们使用反射技术时，下面几条内容应该牢记于心。

- **性能开销** ：反射涉及了动态类型的解析，所以 JVM 无法对这些代码进行优化。因此，反射操作的效率要比那些非反射操作低得多。我们应该避免在经常被执行的代码或对性能要求很高的程序中使用反射。
- **安全限制** ：使用反射技术要求程序必须在一个没有安全限制的环境中运行。如果一个程序必须在有安全限制的环境中运行，如 Applet，那么这就是个问题了。
- **内部暴露** ：由于反射允许代码执行一些在正常情况下不被允许的操作（比如访问私有的属性和方法），所以使用反射可能会导致意料之外的副作用，这可能导致代码功能失调并破坏可移植性。反射代码破坏了抽象性，因此当平台发生改变的时候，代码的行为就有可能也随着变化。

##### 在Java中使用反射主要涉及以下几个步骤：

1. **获取Class对象**：这是反射操作的起点。`Class`对象代表了类的静态属性。可以通过几种方式获取`Class`对象：
   - 使用`Class.forName("完整类名")`方法。例如：`Class.forName("java.lang.String")`。
   - 使用`.class`语法。例如：`String.class`。
   - 使用对象的`getClass()`方法。例如：`"example".getClass()`。
2. **创建实例**：
   - 使用`Class`对象的`newInstance()`方法（在Java 9中已弃用）。
   - 使用`Constructor`对象的`newInstance()`方法，可以处理具有参数的构造函数。
3. **访问字段**：
   - 使用`Class`对象的`getField(String name)`方法获取公共字段，或者`getDeclaredField(String name)`方法获取任何字段（包括私有字段）。
   - 通过`Field`对象的`setAccessible(true)`方法来访问私有字段。
   - 使用`Field`对象的`get()`和`set()`方法来读取和修改字段值。
4. **调用方法**：
   - 使用`Class`对象的`getMethod(String name, Class<?>... parameterTypes)`方法获取公共方法，或者`getDeclaredMethod(String name, Class<?>... parameterTypes)`方法获取任何方法（包括私有方法）。
   - 通过`Method`对象的`setAccessible(true)`方法来访问私有方法。
   - 使用`Method`对象的`invoke(Object obj, Object... args)`方法来调用方法。
5. **处理异常**：反射操作可能会抛出多种异常，例如`ClassNotFoundException`、`NoSuchMethodException`、`IllegalAccessException`等。合理处理这些异常是使用反射的重要部分。

这个示例简单展示了如何通过反射创建`String`对象、调用其方法：

```java
import java.lang.reflect.Method;
import java.lang.reflect.Field;
import java.lang.reflect.Constructor;

public class ReflectionExample {
    public static void main(String[] args) {
        try {
            // 获取Class对象
            Class<?> clazz = Class.forName("java.lang.String");

            // 创建实例
            Constructor<?> constructor = clazz.getConstructor(String.class);
            Object obj = constructor.newInstance("Hello, Reflection!");

            // 访问方法
            Method method = clazz.getMethod("toUpperCase");
            Object result = method.invoke(obj);

            // 输出结果
            System.out.println(result);

            // 访问字段（作为示例，String类没有公共字段）
            // Field field = clazz.getField("someField");
            // field.setAccessible(true);
            // Object fieldValue = field.get(obj);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```



### 泛型

[10 道 Java 泛型面试题](https://cloud.tencent.com/developer/article/1033693)

**简言之**：实现对各种对象操作的类和方法，（允许类和方法同时处理很多类型的对象）

Java中的泛型是一种在编译时提供类型安全检查的机制，它允许在类、接口或方法中使用类型参数（Type Parameters）。泛型的引入增强了Java程序的类型安全性，减少了强制类型转换的需要，并提高了代码的重用性。

例子：

```java
// 泛型类示例
public class Box<T> {
    private T t;

    public void set(T t) {
        this.t = t;
    }

    public T get() {
        return t;
    }
}

// 泛型方法示例
public static <T> T addAndReturn(T element, Collection<T> collection) {
    collection.add(element);
    return element;
}

// 使用
Box<Integer> integerBox = new Box<>();
integerBox.set(10);

List<String> strings = new ArrayList<>();
String stringElement = addAndReturn("Hello", strings);
	
```

#### 泛型的限制

1. **类型擦除**：Java的泛型是在编译时实现的，运行时类型信息会被擦除。例如，`List<String>` 和 `List<Integer>` 在运行时都被视为 `List`。
2. **类型限制**：不能使用基本类型（如 `int`, `float`）作为泛型类型参数，必须使用它们的包装类（如 `Integer`, `Float`）。
3. **不能创建泛型数组**：由于类型擦除，不能创建泛型类型的数组，例如 `new T[]` 是非法的。创建是非法的但是可以使用```T[]```,因为在使用时，编译器是知道他的类型的。



**不意味着**可以接受**任意**类型，因为可以使用各种方式来限制和指导泛型接受的类型：

1. **无限制泛型**：如果没有指定上界，泛型确实可以接受任何类型的对象。例如，`class Box<T>` 可以让 `Box` 类接受任何类型的对象。
2. **有界类型参数**：可以通过有界类型参数限制泛型可以接受的类型。例如，`class Box<T extends Number>` 只接受 `Number` 类及其子类（如 `Integer`、`Double` 等）作为类型参数。
3. **多重边界**：可以指定一个泛型参数必须满足多个限制。例如，`<T extends Number & Comparable<T>>` 表示 `T` 必须同时是 `Number` 的子类，并且实现了 `Comparable` 接口。
4. **通配符限制**：使用通配符（如 `? extends T` 和 `? super T`）可以提供更多的灵活性，允许在使用泛型时限制未知类型的范围。





### Java 各版本的新特性

**New highlights in Java SE 8**

1. Lambda Expressions
2. Pipelines and Streams
3. Date and Time API
4. Default Methods
5. Type Annotations
6. Nashhorn JavaScript Engine
7. Concurrent Accumulators
8. Parallel operations
9. PermGen Error Removed

**New highlights in Java SE 7**

1. Strings in Switch Statement
2. Type Inference for Generic Instance Creation
3. Multiple Exception Handling
4. Support for Dynamic Languages
5. Try with Resources
6. Java nio Package
7. Binary Literals, Underscore in literals
8. Diamond Syntax



### JRE or JDK

- JRE：Java Runtime Environment，Java 运行环境的简称，为 Java 的运行提供了所需的环境。它是一个 JVM 程序，主要包括了 JVM 的标准实现和一些 Java 基本类库。
- JDK：Java Development Kit，Java 开发工具包，提供了 Java 的开发及运行环境。JDK 是 Java 开发的核心，集成了 JRE 以及一些其它的工具，比如编译 Java 源码的编译器 javac 等。

## 

###### ? HashMap实现

###### ? secroized

###### ？java堆内存，栈内存，和对应生命周期

###### ？JVM调优

###### ? 内部类
