



###### 面向对象OOP三大支柱

封装、继承、多态

virtual 和 override 虚函数/重写  ==》多态实现



1、内部类（嵌套） 可以用private protect public 修饰

2、sealed 密封类/密封方法  防止被继承和防止被重写

###### 3、抽象类和接口

抽象类表示的是，这个对象是什么。接口表示的是，这个对象能做什么

 (1) 抽象方法只作声明，而不包含实现，可以看成是没有实现体的虚方法
  (2) 抽象类不能被实例化
  (3) 抽象类可以但不是必须有抽象属性和抽象方法，但是一旦有了抽象方法，就一定要把这个类声明为抽象类
  (4) 具体派生类必须覆盖基类的抽象方法
  (5) 抽象派生类可以覆盖基类的抽象方法，也可以不覆盖。如果不覆盖，则其具体派生类必须覆盖它们

 (1) 接口不能被实例化
  (2) 接口只能包含方法声明
  (3) 接口的成员包括方法、属性、索引器、事件
  (4) 接口中不能包含常量、字段(域)、构造函数、析构函数、静态成员

###### 基类/派生类转换规则

is -a 的关系是隐式转换，永远是类型安全的，（里氏替换原则）

子类=基类，这样需要强制转换。--> as  is

###### 超级父类 System.Object

 virtual bool Equals(Object obj) 被比较指向内存同一个项，则放回true,一般用于比较对象的引用

，如果被重写，如果被比较的对象有相同的内部值状态（基于值的语义），则返回true，eg: string 类重写了该对象，所以字符串是比较字每个字符是否相同。

virtual int GetHashCode()  返回int 标识指定对象的实例，一般Hash 也可用于比较两个对象是否相同。

virtual string ToString()

Object MemberwiseClone()  通常用于克隆对象。

Type GetType()



如果一个类重写了Equals 我们还需要默认重写GetHashCode的实现 ，散列码是表示某个对象某个状态的数字值。

默认情况，GetHashCode 使用对象在内存中的位置来产生散列值。



###### System.Enum  

enum FoodType: short{

}

###### 值类型、引用类型

值类型的可空类型,引用类型不能使用可空类型

bool? nuulbool = false;  对

string? nullstring = null;   错误

###### ？？操作符

一种if/else 更加经凑的写法

int data = cat.getAge()?? 100,如果cat.getAge 返回null, 100作为默认值赋值给变量

###### 对象初始化器  {}



const   隐式静态-   一定要用类调用,       赋值之后不能呗修改

readonly  和常量不同的是，readonly 的值可以在运行时候决定，只能在构造函数的作用域才能合理赋值（其他地方不行）

static readonly  ,因为readonly 不是隐式静态，如果要从类级别公开，则需要显示使用static,

注意，如果要到运行时赋值的话，只能在静态构造函数中赋值

partial ,分布类型的每个部分必须用ｐａｒｔｉａｌ　关键标记

　

###### 委托｜事件｜多播委托｜lambad表达式 | 匿名函数

委托是C#的一种类型，它实际上是一个持有对某个方法的引用的类。

1. 委托允许将方法作为参数进行传递。

2. 委托可用于定义回调方法。

3. delegate是面向对象、类型安全，

4. ,即可指向静态方法，也可指向实例方法

5. delegate => System.MulticastDelegate  => System.Delegate

6.  Method  Target  Comine (+=)  Remove  (-=)  GetInvocationList()

7. C# 委托默认支持多播委托 ，换句话说一个委托对象可以维护一个可调用的方法列表而不是一个单独的方法。

8. 委托是类型安全的，委托协变,允许我们一个委托类型返回子类型：

   ​	public deletage Car ObtainVehicleDeleagte();    SportCar 继承于Car

   ​	public Car GetBaseCar(){}     public SportCar GetSportCar(){},两个函数都可以是ObtainVehicDelegate的安全类型。

**Event** C# 事件是一种特殊的委托实例对象，可保证触发只能在模块内部触发，外部只能注册和移除函数，外部无法触发。event 就像一块语法糖，节省了我们打字的时间。

**匿名方法**： 事件注册时直接将一个委托和一段代码相关联。

​					匿名方法不能访问定义方法中的ref  out 参数

​					匿名方法的本地变量不能和外部方法同名

​					匿名方法可以访问外部类作用域的实例变量

​					+= delegate(){                                            };

**Lambad**  表达式实质上是一个匿名函数，是一种一种更简单的写法的匿名函数。

**多播委托**  C# 委托默认就只是继承多播委托的类的，一个委托对象可以维护一个可调用的方法列表而不是一个单独的方法。  有点像订阅发布者模式一样

###### using 

处理实现了IDisposable 的托管对象时候，原理==》， try{}finally{ xx.Dispose()}

如果一个对象未实现IDispose的对象 使用using ，将收到编译器的错误



###### 延迟对象实例化

Lazy<xxx>  all sound = new Layz<xxx>();

sound 直到被其他调用的时候才会被实例化。



###### IEnumerable 和  IEnumerator



public interface IEnumrable{

​	IEnumrator GetEnumrator();

}

public interface IEnumtator{

​	bool MoveNext();

​    object Current{get;}

   void Reset();

}

###### ICloneable  返回的是浅拷贝



###### IComparable 和 IComparaer





###### 高级C# 语法特性

- 属性  get set

- 索引器   public xxx this[string name] {get xxx;set xxx;}    索引器重载

- 操作符重载  public static Point operator - (Point a ,Point b){   return xxx}

- 显示转换和隐式转换重载  explicit  implicit

  ​		public static explicit operator Square(int sideLength){ return new Sequare(sideLength);}

  ​	    public static explic operator int(Square square){return square.Length;}

- 扩展方法 静态类、静态方法 、this关键字

  ​       public  static int  SlowDown(this Car c){ return --c.speed;}

- 指针类型  可以绕开CLR 的内存管制机制 unsafe fixed sizeof(值类型)



###### C# 集合

1、 非泛型集合  ：   HashTable  ArrayList  Queue  SortedList    Stack  

| ICollection | 非泛型集合的基本定义（大小，枚举、线程安全）   |
| ----------- | ---------------------------------------------- |
| ICloneable  | 允许实现它的对象向调用者返回它的副本           |
| IDictionary | 允许非泛型集合使用Key/Value 来表示其内容       |
| IEnumerable | 返回 实现了  IEnumerator接口的对象             |
| IEnumerator | 允许 类型 foreach 形式迭代                     |
| IList       | 为顺序列表中的对象提供添加、移除、和索引项行为 |



2、泛型集合：Dictionary<TKey,TValue>   List<T> （动态该表大小的顺序列表）  LinkedList<T> (双向列表)   Queue<T>   Stack<T>    SortedLSet<T>  （一个排序的不重复 的对象集合）   SortedDictionary<TKey,TValue>（一个排序了的键值对的泛型集合）

| ICollection<T>           | 为所有泛型集合的基本定义（大小，枚举、线程安全） |
| ------------------------ | ------------------------------------------------ |
| IComparer<T>             | 定义比较对象的方式                               |
| IDictionary<TKey,TValue> | 允许泛型集合使用Key/Value 来表示其内容           |
| IEnumerable<T>           | 返回 实现了  IEnumerator<T>接口的对象            |
| IEnumerator<T>           | 允许 类型 foreach 形式迭代                       |
| IList<T>                 | 为顺序列表中的对象提供添加、移除、和索引项行为   |
| ISet<T>                  | 为抽象的集提供基接口                             |



泛型约束 ：  where T :struct/class/:new(){默认的构造函数} /XXXClass/XXXInteface

多项约束 ：   where T : class,IDrawable,new()

泛型约束不足：where T :operator +,operator -,operator *,operator / 



非泛型集合和泛型集合优缺点

泛型集合提供更好的性能，没有装箱和拆箱的消耗

泛型集合更加类型安全

泛型集合大幅减少了构建自定义集合类型的需求

非泛型集合可以存储任意类型，十一个及其灵活的容器，缺点相对泛型集合的优点的反面



**HashTable 的实现原理，复杂度是多少**?  **增加 删除 获取 时间复杂度**？

1. 速度查询速度快，而添加速度相对   原因a，添加元素时可能会地址冲突，需要重新定位地址 。 b，扩容后 数组拷贝，重新哈希计算旧数组所有key。
2. 慢装填因子 = 0.72，这个比值太大会造成冲突概率增大，太小会造成空间的浪费。默认是0.72
3. HashTable 元素不是顺序的，
4. 内部数据桶（数组）默认长度=3，长度一定是素数； 为什么扩容的数组长度一定要是素数呢？因为素数有一个特点，只能被自己和1整除，如果不是素数那么在进行取模计算的时候可能会出现多个值

HashTable的原理

1、先判断当前元素个数于bucket数组之比是否超过0.72

 小于 0.72 :对 key进行哈希取值，将得到的与bucket数组的长度进行取模计算，s将取模的结果插入到bucket数组对应的索引，将 value 赋值到其对应的value.

​		因为哈希值可能会重复，从而导致地址冲突，HashTable Hashtable 采用的是 "开放定址法" 处理冲突， 具体行为是把 HashOf(k) % Array.Length 改为 (HashOf(k) + d(k)) % Array.Length  得出另外一个位置来存储关键字 "a" 所对应的数据, d 是一个增量函数. 如果仍然冲突, 则再次进行增量, 依此循环直到找到一个 Array 中的空位为止。

大于  0.72：对bucket数组进行扩容，

​		a、创建一个新数组扩容大小应该是2倍于当前容量最小的素数；eg:length=3  new length = 7

​		b、将原来数组元素拷贝到新的数组中，因为bocket数组长度变了，所以需要对所有key重新哈希计算（这是影响hashtable性能的重要因素）。

​		c， 进行上面a步骤。



###### Q:C# 如何创建一个对象?

A、首先计算分配对象需要的总内存大小

B、检查托管堆，确保有足够的空间分配对象。如果足够，则调用类的构造方法，将托管堆内存中新对象的引用返回给调用者，在返回之前移动托管堆的指针，指向托管的下一个可用的位置。

 

###### Q:GC理解?

A、采用标记压缩策略。在一次垃圾回收过程中，运行库将检查托管堆上的对象，判读应用程序是否任然可以访问它们（即：对象是否还有跟），如果对象不可访问，则会标记为垃圾对象，它们将从对象中清除。托管堆上的内存空间将会被压缩，最后“托管堆的下一个对象”指针将重新指下一个可用的位置。

B、对象的“代”的，托管堆上所有对象都有属于自己“代”。设计思路很简单，对象在运用程序存在的时间越久，它就更有可能被保留下来。.Net 将托管堆上的对象中分为3代。第0代，重来没标记回收的新对象。第1代，上次垃圾回收没被回收的对象。第2代，在上一次垃圾回收没被回收的对象。垃圾回收器，分别从第0 1 2 代去调查对象。每一代的调查频率不同。概率大概1000:10：1。



###### Q:装箱拆箱的理解

装箱：值类型     -> 引用类型

拆箱：引用类型  -> 值类型              装箱、拆箱都会引起  GC 和 性能损耗。

