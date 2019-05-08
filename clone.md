# Clone

## 为什么要clone
实现基本类型的变量复制很简单, 但是复制对象类型得到的只是引用的复制, 即复制一份地址, 
仍旧时指向堆内存上的同一个对象

## 如何实现clone

### ShallowClone
通过实现Cloneable接口可以实现浅克隆, 浅克隆得到的克隆对象的对象属性仍旧是克隆的引用

1. 新建Cloneable接口的实例类
2. 重写clone()方法, 并调用父类的clone()方法
```
@Override
public Object clone() {
    Student stu = null;
    try{
        stu = (Student)super.clone();
    }catch(CloneNotSupportedException e) {
        e.printStackTrace();
    }
    return stu;
}
```

### DeepClone
通过序列化和反序列化实现深度克隆, 会得到一个对象的完全克隆, 对象与克隆之间不会相互影响
1. 创建序列化工具类, 将输入的对象序列化之后, 再反序列化然后返回
```
public class MyUtil {

    private MyUtil() {
        throw new AssertionError();
    }
    public static <T> T clone(T obj) throws Exception {
        //将传入的对象序列化
        ByteArrayOutputStream bout = new ByteArrayOutputStream();
        ObjectOutputStream oos = new ObjectOutputStream(bout);
        oos.writeObject(obj);
        //将对象反序列化,并返回
        ByteArrayInputStream bin = new ByteArrayInputStream(bout.toByteArray());
        ObjectInputStream ois = new ObjectInputStream(bin);
        return (T) ois.readObject();
    }
}
```
2. 调用该类的clone()方法, 输入需要深度克隆的对象
