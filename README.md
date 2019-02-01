## 单例设计模式
### 什么是singleton?
Singleton：在Java中即指单例设计模式，它是软件开发中最常用的设计模式之一。

- 单：唯一
- 例：实例

单例设计模式，即某个类在整个系统中只能有一个实例对象可被获取和使用的代码模式。

- 例如：代表JVM运行环境的Runtime类

### 要点
- 某个类只能有一个实例（构造器私有化）
- 它必须自行创建这个实例（含有一个该类 的静态变量来保存整个唯一的实例）
- 它必须自行向整个系统提供这个实例（对外提供获取该实例对象的方式：1、直接暴露 2、用静态变量的get方法获取

### 几种常见的形式
### 饿汉式：直接创建对象，不存在线程安全问题
- 直接实例化饿汉式（简洁直观）
- 枚举式（最简洁）
- 静态代码块饿汉式（适合复杂实例化）

### 懒汉式：延迟创建对象
- 线程不安全（适用于单线程）
- 线程安全（适用于多线程）
- 静态内部类形式（适用于多线程）

### 总结
- 如果是饿汉式，枚举形式最简单
- 如果是懒汉式，静态内部类形式最简单

## 类初始化和实例初始化
![](https://github.com/geekerstar/dive-in-interview/blob/master/img/1.jpg)

![](https://github.com/geekerstar/dive-in-interview/blob/master/img/2.jpg)

![](https://github.com/geekerstar/dive-in-interview/blob/master/img/3.jpg)

### 考点？
- 类的初始化过程
- 实例初始化过程
- 方法的重写

### 类初始化的过程
#### 一个类要创建实例需要先加载并初始化该类
- main方法所在的类需要先加载和初始化
#### 一个子类要初始化需要先初始化父类
#### 一个雷初始化就是执行<clinit>()方法
- <clinit>()方法由静态类变量显示赋值代码和静态代码块组成
- 类变量显示赋值代码和静态代码块代码从上到下顺序执行
- <clinit>()方法只执行一次

### 实例初始化过程
#### 实例初始化就是执行<init>()方法
- <init>()方法可能重载有多个，有几个构造器就有几个<init>方法
- <init>()方法由非静态实例变量显示赋值代码和非静态代码块、对应构造器代码组成
- 非静态实例变量显示赋值代码和非静态代码块代码从上到下顺序执行，而对应构造器的代码最后执行
- 每次创建实例对象，调用对应构造器，执行的就是对应的<init>方法
- <init>方法的首行是super()或super(实参列表)，即对应父类的<init>方法

### 方法的重写Override
#### 哪些方法不可以被重写

- final方法
- 静态方法
- private等子类中不可见方法

#### 对象的多态性
- 子类如果重写了父类的方法，通过子类对象调用的一定是子类重写过的代码
- 非静态方法默认的调用对象是this
- this对象在构造器或者说<init>方法中就是正在创建的对象

### 总结
- Override和Overload的区别？
- Override重写的要求？（方法名、形参列表、返回值类型、抛出的异常列表、修饰符）
- 了解《JVM虚拟机规范》中关于<clinit>和<init>方法的说明、invokespecial指令

## 方法的参数传递机制
![](https://github.com/geekerstar/dive-in-interview/blob/master/img/4.jpg)

![](https://github.com/geekerstar/dive-in-interview/blob/master/img/5.jpg)

### 考点
- 方法的参数传递机制
- String、包装类等对象的不可变性

### 方法的参数传递机制
#### 形参是基本数据类型
- 传递数据值
#### 实参是引用数据类型
- 传递地址值
- 特殊的类型：String、包装类等对象不可变性

![](https://github.com/geekerstar/dive-in-interview/blob/master/img/8.png)


## i++和++i
![](https://github.com/geekerstar/dive-in-interview/blob/master/img/7.jpg)

- 赋值=，最后计算
- =右边的从左到右加载值依次压入操作数栈
- 实际先算哪个，看运算符优先级
- 自增、自减操作都是直接修改变量的值，不经过操作数栈
- 最后的赋值之前，临时结果也是存储在操作数栈中

> 建议：《JVM虚拟机规范》关于指令的部分

## 编程题：有n步台阶，一次只能上1步或2步，共有多少种走法？

- 递归
- 循环迭代

### 总结
方法调用自身称为递归，利用变量的原值推出新值称为迭代。

#### 递归
- 优点：大问题转化为小问题，可以减少代码量，同时代码精简，可读性好；
- 缺点：递归调用浪费了空间，而且递归太深容易造成堆栈的溢出。
#### 迭代
- 优点：代码运行效率好，因为时间只因循环次数增加而增加，而且没有额外的空间开销；
- 缺点：代码不如递归简洁，可读性好


## 成员变量与局部变量
```java
public class Variable {
    /**
     * 成员变量，类变量
     */
    static int s;
    /**
     * 成员变量，实例变量
     */
    int i;
    /**
     * 成员变量，实例变量
     */
    int j;
    {
        //非静态代码块中的局部变量 i
        int i = 1;
        i++;
        j++;
        s++;
    }
    public void test(int j){//形参，局部变量,j
        j++;
        i++;
        s++;
    }
    public static void main(String[] args) {//形参，局部变量，args
        //局部变量，obj1
        Variable obj1 = new Variable();
        //局部变量，obj1
        Variable obj2 = new Variable();
        obj1.test(10);
        obj1.test(20);
        obj2.test(30);
        System.out.println(obj1.i + "," + obj1.j + "," + obj1.s);
        System.out.println(obj2.i + "," + obj2.j + "," + obj2.s);
    }
}

```

```text
2,1,5
1,1,5
```

### 考点
#### 就近原则
#### 变量的分类
- 成员变量：类变量、实例变量
- 局部变量
#### 非静态代码块的执行：每次创建实例对象都会执行
##### 方法的调用规则：调用一次执行一次

### 局部变量与成员变量的区别
#### 1、声明的位置
局部变量：方法体{}中，形参，代码块{}中

成员变量：类中方法外
- 类变量：有static修饰
- 实例变量：没有static修饰
#### 2、修饰符
局部变量：final

成员变量：public、protected、private、final、static、volatile、transient
#### 3、值存储的位置
局部变量：栈

实例变量：堆

类变量：方法区

#### 4、作用域
局部变量：从声明处开始，到所属的}结束

实例变量：在当前类中“this.”(有时this.可以缺省)，在其他类中“对象名.”访问

类变量：在当前类中“类名.”(有时类名.可以省略)，在其他类中“类名.”或“对象名.”访问

#### 5、生命周期
局部变量：每一个线程，每一次调用执行都是新的生命周期

实例变量：随着对象的创建而初始化，随着对象的被回收而消亡，每一个对象的实例变量是独立的

类变量：随着类的初始化而初始化，随着类的卸载而消亡，该类的所有对象的类变量是共享的


### 当局部变量与xx变量重名时，如何区分
#### 局部变量与实例变量重名
- 在实例变量前面加“this.”
#### 局部变量与类变量重名
- 在类变量前面加“类名.”

![](https://github.com/geekerstar/dive-in-interview/blob/master/img/9.png)


## bean的作用域之间有什么区别？

可以通过scope属性来指定bean的作用域
- singleton：默认值。当IOC容器一创建就会创建bean的实例，而且是单例的，每次得到的都是同一个
- prototype：原型的。当IOC容器一创建不再实例化该bean，每次调用getBean方法时再实例化该bean，而且每调用一次创建一个对象
- request：每次请求实例化一个bean
- session：在一次会话中共享一个bean


## Spring支持的常用数据库事务传播属性和事务隔离级别
@Transactional注解
 * 	该注解可以添加到类上，也可以添加到方法上
 * 	如果添加到类上，那么类中所有的方法都添加上了事务
 * 	如果添加到方法上，只有添加了该注解的方法才添加了事务
 
### 请简单介绍Spring支持的常用数据库事务传播属性和事务隔离级别？
事务的属性：

1.propagation：用来设置事务的传播行为
- 事务的传播行为：一个方法运行在了一个开启了事务的方法中时，当前方法是使用原来的事务还是开启一个新的事务
- Propagation.REQUIRED：默认值，使用原来的事务
- Propagation.REQUIRES_NEW：将原来的事务挂起，开启一个新的事务

2.isolation：用来设置事务的隔离级别
- Isolation.REPEATABLE_READ：可重复读，MySQL默认的隔离级别
- Isolation.READ_COMMITTED：读已提交，Oracle默认的隔离级别，开发时通常使用的隔离级别

## SpringMVC中如何解决POST请求中文乱码问题
