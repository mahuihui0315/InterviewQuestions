 # container

## java容器都有哪些

### List
+ ArrayList：可以存储任意类型元素，包括null，容量大小会自动增加，非线程安全
+ LinkedList：双向链表，可以用做队列或者双端队列
+ Stack：先入后出的栈
+ Vector：相对于ArrayList，该动态数组类线程安全

### Set
+ HashSet：存储元素无序，允许null，非线程安全，通过hashcode确定元素的存储位置
   + LinkedHashSet：元素存储有序，由内部的双向链表维护元素的顺序，使用hashcode确定元素的位置，非线程安全
+ TreeSet：存储元素有序，通过CompareTo方法来确定元素的存储顺序
### Queue
特殊的线性表，只允许在表头删除元素，在表尾添加元素，即先进先出原则
#### 非阻塞
不支持阻塞的队列
+ LinkedList：双向链表，实现了queue接口，因此可以当做queue使用
+ PriorityQueue: 从小到大排序好的列表 逻辑结构是一棵完全二叉树
+ ConcurrentLinkedQueue: 是一个线程安全的并发不需要同步的线程
#### 阻塞
阻塞的定义：
+ 阻塞插入：当队列中的元素满了，插入操作线程将阻塞直至队列有空闲空间
+ 阻塞删除：当队列中的元素为空，就是指没有元素时，移除操作线程将阻塞直至队列不为空

支持阻塞的队列
+ ArrayBlockingQueue：一个由数组支持的有界队列
+ LinkedBlockingQueue：一个由链接节点支持的可选有界队列
+ PriorityBlockingQueue：一个由优先级堆支持的无界优先级队列
+ DelayQueue：一个由优先级堆支持的，基于时间的调度队列

### Map
以key-value即键值对的形式储存数据，key唯一不允许重复
+ HashMap：最常用的map，根据key的hashcode存储元素，可通过key迅速访问值，最多允许一条记录的key为null，重复添加会覆盖，非线程安全
+ HashTable：不同于HashMap，key，value均不能为null，线程安全，因此速度比HashMap要慢
+ TreeMap：会根据key对元素进行排序，默认为升序，key不允许为null，非线程安全
+ LinkedHashMap：保存元素的插入顺序，key和value都允许为null

## Collection和Collections的区别

### Collection
最基本的集合接口，list、set均继承于collection

### Collections
一个针对集合操作的工具类，方法都是静态的

常用方法：
+ public static \<T> void sort(List\<T> list)：排序，默认情况下是自然顺序。
+ public static \<T> int binarySearch(List\<?> list,T key)：二分查找
+ public static \<T> T max(Collection\<?> coll)：最大值
+ public static void reverse(List\<?> list)：反转
+ public static void shuffle(List\<?> list)：随机置换

## List、Set、Map的区别

### List
1. 元素按照插入顺序有序存储
2. 可以允许重复元素
3. 可以存储多个null

### Set
1. 元素存储无序，但是TreeSet实现了SortedSet接口，可以通过CompareTo函数确定元素顺序
2. 不允许重复元素
3. 只允许最多一个null元素

### Map
map不同于list和set，并不是collection的实现类，而是一个单独的map接口

1. 以键值对的方式存储数据
2. 无序存储，但是TreeMap也通过Comparator实现了排序
3. map允许最多一个key为null，value可以有多个null

### 适用场景
1. 经常使用索引进行访问的场景，更适合list的实现类，例如ArrayList；同时如果经常删除元素，可以使用LinkedList
2. 需要保证元素的插入顺序，list是一个有序集合，因此比较合适
3. 保证插入的元素的唯一性，则set的实现类比较适合
4. 如要用到键值对的存储方式，可以从map的实现类中选择合适的

## HashMap 的实现原理
基本原理：数组+链表+红黑树

+ Entry数组：用于存储key-value对，每一个key-value就是一个Entry实体
+ Entry类：本质是是一个链表，具有Next属性用于指向下一个Entry。
因为key-value的存储位置是由key的hashcode决定的，因此可能回出现位置相同的情况，此时就可以使用Next来解决位置冲突
+ 红黑树：JDK8以后引入，当链表过长时会转化成红黑树

## HashSet 的实现原理
hashset是基于hashmap实现的，底层使用hashmap实现

## ArrayList 和 LinkedList 的区别

### 在末尾增加元素
+ ArrayList: 
   + 底层实现是数组, 初始化时会有一定的容量, 当容量未满时插入效率很高, 但是一旦容量不够就需要扩容, 基本原理是复制当前
的数组元素到一个新的更大容量的数组, 此时效率很低
+ LinkList:
   + 底层实现是一个双向链表, 新增元素时不需要考虑容量问题, 效率一直很高

### 在中间增减元素
+ ArrayList:
   + 插入位置之后的元素都需要向后移动, 效率很差, 插入越靠前越是如此
+ LinkList:
   + 对于链表来说在任何位置插入元素的效率都很高

### 移除任意元素
+ ArrayList:
   + 移除元素和插入元素一样, 都需要重组数组, 因此效率不高, 且越靠前越差
+ LinkList:
   + 链表移除元素需要先遍历寻找目标元素的位置, 因此效率会和链表的长度以及元素的位置相关
   
### 访问任意元素
+ ArrayList: 
   + 数组可以通过下标快速访问元素, 效率很高
+ LinkList: 
   + 链表每次访问数据都要进行遍历操作, 十分费时
   
## 数组和 List 之间的转换
+ 数组转List: Arrays的asList()
+ List转数组: toArray()

## ArrayList 和 Vector 的区别
+ ArrayList: 
   1. 非线程安全, 因此效率更高
   2. 扩容时会增加50%的容量
+ Vector:
   1. 线程安全, 效率稍差
   2. 扩容时会增加100%的容量
   
## Array 和 ArrayList 的区别
1. Array可以包含基本类型和对象类型, ArrayList只能包含对象类型
2. Array容量固定, ArrayList容量会动态改变
3. ArrayList提供了更多操作数据的方法

## Queue 中 poll()和 remove()的区别
+ poll(): 移除队列顶端的元素, 当队列为空时返回null
+ remove(): 移除队列顶端的元素, 当队列为空时抛出异常

## 使一个集合不能被修改
使用Collections.unmodifiableList(List<? extends T> list)
