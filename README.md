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

## i++和++i
![](https://github.com/geekerstar/dive-in-interview/blob/master/img/7.jpg)

- 赋值=，最后计算
- =右边的从左到右加载值依次压入操作数栈
- 实际先算哪个，看运算符优先级
- 自增、自减操作都是直接修改变量的值，不经过操作数栈
- 最后的赋值之前，临时结果也是存储在操作数栈中

> 建议：《JVM虚拟机规范》关于指令的部分

