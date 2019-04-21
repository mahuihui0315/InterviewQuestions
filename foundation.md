# Foundation of Java

## JDK和JRE的区别

### JDK
Java Development Kit，java开发包，面向编程人员，内含JRE（Java Runtime Environmen）包括client和server端，使用前需要配置环境变量

### JRE
Java Runtime Environmen，java运行环境，顾名思义就是java程序运行所必需的，会自动配置环境变量，并不面向编程，知识提供运行环境

## ==和equals的区别

### ==
判断两个对象或者引用是否指向内存中的同一位置，即判断是否是同一个对象

### equals
一般判断两个对象是否值是否相同，可有开发人员重写以自定义判断条件

## hashCode()相同，equals()是否为true
不一定，两个不同对象通过hashcode函数获取的值有可能相同

但是反过来，equals为true则hashCode一定相同

## final的作用
+ 修饰变量
   1. 基本类型：该变量一旦复制就无法改变，成为常量
   2. 引用类型：该引用无法指向其他引用，但是被指向的对象可以改变
+ 修饰方法：该方法无法被重写
+ 修饰类：该类无法被继承
   1. 该类下的方法也会被隐式的指定为final
   2. 成员变量不受影响
   
## Math.round(-1.5)的值
值为-1，因为四舍五入取较大的一方，-1要比-2大

## String的数据类型
string是属于final修饰的java类，并不是基本数据类型

+ 整型：short、int、long
+ 浮点类型：float、double
+ 字符型：byte、char
+ 布尔类型：boolean

## 操作字符串的常用类

### String
最基本的字符串类，为final修饰，存储方式是字符数组，每次修改都会产生一个新的字符串，原有字符串不受影响

### StringBuffer
线程安全的字符串类，其添加元素的方法append是在原字符串基础上修改的，因此效率比string高

### StringBuilder
线程不安全的字符串类，append方法同StringBuffer，但是因为放弃synchronized的线程安全功能，效率比StringBuffer高

## String str="a"与 String str=new String("a")的区别

### String str1= “a”
在编译期，JVM会去常量池来查找是否存在“a”，如果不存在，就在常量池中开辟一个空间来存储“a”；如果存在，就不用新开辟空间。然后在栈内存中开辟一个名字为str1的空间，来存储“a”在常量池中的地址值。

### String str=new String("a")
在编译阶段JVM先去常量池中查找是否存在“a”，如果过不存在，则在常量池中开辟一个空间存储“a”。在运行时期，通过String类的构造器在堆内存中new了一个空间，然后将String池中的“a”复制一份存放到该堆空间中，在栈中开辟名字为str2的空间，存放堆中new出来的这个String对象的地址值

## 如何将字符串反转
1. 遍历然后倒序输出
2. 创建StringBuilder类型，使用reverse方法进行翻转，然后toString

## String类的常用方法
1. char charAt(int index)
2. int compareTo(String str)
3. int compareToIngoreCase(String str)
4. boolean contains(CharSequence str)
5. static String copyValueOf(char[] chars)
6. int indexOf(int ch)
7. int lastIndexOf(int ch)
8. int length()
9. char[] toCharArray();
10. String subString(int beginIndex,int endIndex)

## 抽象类与抽象方法方法的关系
抽象类不一定要有抽象方法，但是抽象方法一定在抽象类中

## 普通类和抽象类的区别
1. 抽象类不能被实例化
2. 可以有构造函数，被继承时子类必须继承父类的一个构造函数
3. 抽象方法不能被声明为静态，因为静态方法需要该类的实例调用，而抽象类无法实例化
4. 抽象方法不需强制实现，抽象类中可以有普通方法
5. 抽象类的子类必须实现所有 抽象方法，否则这个子类也是抽象的

## 抽象类和接口的区别
1. 抽象类有构造函数，而接口没有
2. 抽象类可以实现方法，而接口不行
3. 抽象类的方法可以使用public、protecte和default这些修饰 ，而接口默认public也只能时public
4. 抽象类可以有属性，而接口不行

## IO流

### 字节流
以字节为单位，可以读取所有数据，其具体子类查看API
+ InputStream
+ OutputStream

### 字符流
以字符为单位，只能处理字符类型数据，其具体子类查看API
+ Reader
+ Writer

## File类的常用方法

### 创建
+ boolean createNewFile()：创建新的空文件
+ boolean mkdir()：创建单个文件夹
+ boolean mkdirs()：创建多级文件夹
+ boolean renameTo(File dest)：重命名或者剪切文件

### 删除
+ Boolean delete()

### 判断
+ boolean exists()：文件或文件夹是否存在
+ boolean isFile()：是否是一个文件，如果不存在，则始终为false
+ boolean isDirectory()：是否是一个目录，如果不存在，则始终为false

### 获取
+ String getName()：获取文件或文件夹的名称，不包含上级路径
+ String getAbsolutePath()：获取文件的绝对路径，与文件是否存在没关系
+ long length()：获取文件的大小（字节数），如果文件不存在则返回0L，如果是文件夹也返回0L
+ String getParent()：返回此抽象路径名父目录的路径名字符串；如果此路径名没有指定父目录，则返回null
+ long lastModified()：获取最后一次被修改的时间。