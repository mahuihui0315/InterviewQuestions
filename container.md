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

