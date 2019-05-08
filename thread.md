# Thread

## 并行和并发的区别
+ 并发: 同一个CPU上在不同线程之间切换
+ 并行: 不同CPU上同时进行线程

## 线程和进程的区别
+ 进程: 运行在计算机上的一个应用就是一个进程, 可以拥有多个线程
+ 线程: 进程中的一个每一个任务, 进程中运算的最小单位, 只能有一个进程

## 守护线程
属于服务线程, 用于服务其他的线程, 例如垃圾回收机制

## 创建线程的方式

### 继承Thread
1. 新建类继承Thread
2. 重写run()方法
3. 调用该线程对象的start()方法开启线程

### 实现Runnable接口
1. 创建Runnabe接口的实现类
2. 重写run()
3. 创建实例对象, 作为参数传入Thread, 并调用start()方法
```
RunnableImplement imp=new RunnableImplement();
new Thread(imp,"threadName").start();
```
4. 或者使用Executor
```
ExecutorService executor=Executors.newCachedThreadPool();
executor.execute(new RunnableImplement());
executor.shutdown();
```

## 实现Callable接口
1. 创建Callable接口的实现类
2. 重写call()方法, 返回类型为实现接口时定义的类型
3. 使用ExecutorService.submit()方法调用, 并返回Future类型数据, 并可以使用get()获取数据

## 线程的状态
1. 初始化状态: new一个实例,但并未进行任何操作
2. 可运行状态: 
   1. 调用了start()方法即进入可运行状态, 但并不一定会立即运行
   2. 当前线程sleep()方法结束, 等待其他线程
   3. 当前线程时间片段用完, 调用了yield()方法
   4. 锁池的线程对象拿到锁后
3. 运行状态: 线程调度机制分配给当前线程运行时间, run()方法被调用
4. 死亡状态: 
   1. run()方法运行完毕
   2. main()方法运行完毕
5. 阻塞状态: 
   1. 当前线程调用了sleep()方法
   2. 等待用户输入的时候

## 线程池的状态
1. Running: 可以接受新任务, 并处理已添加的任务
2. Shutdown: 不接受新任务, 但可以继续处理已添加的任务
3. Stop: 既不接受新任务, 也不会继续处理已添加的任务
4. Tidying: 所有的任务都已终止, 任务数量为0时, 线程池会处于Tidying状态
5. Terminated: 线程池彻底终止

## submit和execute的区别
+ submit: 用于执行又返回值得线程, 返回一个Future对象, 使用get()获取返回值
+ execute: 执行不需要返回值的线程, 效率更高

## ThreadLocal
为变量在线程生成一个, 用以解决多线程访问共享变量的问题