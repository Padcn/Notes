# JAVA 开发环境配置及面向对象概念
## jdk配置
分为两步:
1. 下载安装jdk
2. 配置环境变量:
    CLASSPATH环境变量在jdk1.6之后可以不用配置了。但是如果想直接在命令行中运行还是最好配置一下。
    目的是为了操作系统能够识别jdk/bin下的程序。
### windows下
1. oracle官网下载jdk,现在都是exe可执行文件了，直接运行安装。
  http://www.oracle.com/technetwork/java/javase/downloads/index.html

2. 计算机->属性->高级系统设置->高级->环境变量。
  举例:(jdk安装路径为d:/jdk)则环境变量设置如下（等号前为新建变量名，等号后为变量的值）:

  ​	JAVA_HOME=d:\jdk
  	CLASSPATH=.;d:\jdk\lib
  	PATH=<这里为原先path的值>;%JAVA_HOME%\bin;

  这里主要目的是为了将安装的路径加入PATH中，JAVA_HOME和CLASSPATH只是中间的变量。偷懒可以直接把全路径添加到PATH的末尾,但是这样就不好管理。
3. 完成环境变量的配置后可以按win+r 输入cmd之后打开命令行后输入'java -version'进行验证如果输入没有该命令则配置没有成功,仔细检查配置的路径修改.成功则会显示jdk的版本号。

### linux下 
linux下可以直接使用软件包管理器安装openjdk，也可以去oracle下载jdk。
对于直接使用包管理器安装的安装完就完事了。
如果自己去oracle下载的则需要解压到想要存放的位置，后配置下环境变量。
假设解压后存放位置在/usr/java/jdk.则在/etc/profile文件末尾加上以下内容
可以用命令` vim /etc/profile `编辑，或者新手可以使用` nano /etc/profile `

```bash
export JAVA_HOME=/usr/java/jdk
export ClASSPATH=.:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```
> 这里CLASSPATH不配置的话在命令行中无法直接运行编译后的class文件，提示为找不到加载类,如果实在不想配可以 使用` java -cp ./<class文件的路径>`,手动制定classpath临时运行.
添加完之后加载修改后的文件
```bash
source /etc/profile
# 校验是否安装成功,输出版本信息则为成功
java -version
```

## HelloWorld
配置完后总不能什么都不干,拿起顺手的编辑器写一个helloworld吧。
@HelloWorld.java
```java
public class HelloWorld{
	public static void main(String args[]){
		System.out.println("Hello World!");
	}
}
```
保存为HelloWorld.java后使用javac编译
```bash
javac HelloWorld.java
```
编译完后生成一个HelloWorld.class文件。

```bash
java HelloWorld
```

运行写好的HelloWorld屏幕上打印出了HelloWorld。



## 概念

java是一种面向对象的高级编程语言，这里的高级指的是层次比较高，相对应的词是底层，底层的语言比较靠近机器语言，如汇编，而高级则比较容易被人理解，c++,c,java等都是。

有一句话是世间万物皆对象：面向对象是一种思考的方式，比如

面向过程:c语言就是一个面向过程的语言。下面c语言的程序结构。从main函数开始依次输出Hello world,然后返回0，从上到下一步一步执行。记得大学里的时候老师举的例子是传送带，现在干什么下一步干什么，注重这个过程。

```c
#include<stdio.h>
int main(){
	printf("Hello");
	return 0;
}
```

而面向对象则则是注重这个对象，这里有个人，他可以干什么，下面是java的一个示例：

```java
//这里我们定义了一个类型，就是人这个类型
public class People{
    //每个人应该都有一个名字，在人这个类里面加一个name
    public String name;
   //大部分人都能说话，所以定义一个说话方法，表示这个类可以进行的动作。
    public void speak(){
        System.out.printf("Hello!I am"+name);
    }
    
    public static void main(String args[]){
        People p=new People();
        p.name="ZhangSan";
        p.speak();
    }
}
```

这里用面向对象的解释是：最开始我们定义了一个类型 People，我们定义是人就应该有个名字，所以给了他一个属性， 这里我们创建了一个人p，并且给了他一个名字ZhangSan,这个人说了一句话。

而用面向过程的方式解释就是:创建了一个变量，给变量赋值，调用了一个方法，结束。



面向对象，面向过程都是一种用来看待事物的方式，当然还有一种是面向切面，这里就不扩展了。



类和对象：高级语言使用类这种单元管理数据。

因为java是基于面向对象的语言，所以所有的类都有一个父类型，就是Object。比如人类是一种动物,则动物类型是人类型的父类。



面向对象三种特性： 

### 封装

什么是封装？

就是把一个类的属性和方法都包装到类中，对外隐藏具体实现，而对外开放接口，供其他类进行调取，而不用关心具体实现。比如，对大多数人来说只要会用键盘，鼠标等外设操作电脑就可以了，而不用去关心，电脑内部的总线，寄存器是干嘛用的，电脑内每一个零件的作用对于用户来说并不重要，转而去做自己应该做的工作。

为什么要封装？
隐藏实现的细节，对外提供公共的方法，优点是增加代码的可维护性，数据的安全性。

怎么实现封装?

java中使用访问修饰符进行实现访问的限制,以下表格为各个修饰符对于修饰对象的访问控制，default为不加修饰符情况下。

|           | 本类 | 同包 | 继承 | 所有 |
| --------- | ---- | ---- | ---- | ---- |
| public    | √    | √    | √    | √    |
| protected | √    | √    | √    | ×    |
| default   | √    | √    | ×    | ×    |
| private   | √    | ×    | ×    | ×    |

### 继承

为什么要继承？

实现了抽象，增加了代码的可复用性。

假设我们有一个人的类型，现在又需要一个动物的类型，而人包含在动物这个类型中，那动物能做的动作在人类中还要重新写一次，很浪费时间，这时候就需要继承。继承顾名思义，就是从一个类型中继承下来部分特性，比如 动物可以运动，而人是动物，所以人可以运动。

使用关键字`extends` 来继承，这样People类型就可以直接调用Animal的运动方法了。

```java
class Animal{
    public void move(){
        System.out.println("走了一步");
    }
}
class People extends Animal{
}
```

当然java并不能阻止你乱继承，人继承植物他也不会报错。但是这样带来的是层次的混乱。

一般继承的原则是符合   子类 是  父类 则继，如 "人"是"动物"。合理的继承会让程序清晰。另一方面，有一点需要注意的是继承层次越复杂，程序的效率会越低。

在java中并不能像C++那样多继承，但由于单继承扩展性比较差，可以通过接口(interface)实现多继承。比如一个超人可以同时继承人的思想和鸟类的飞行等，但是可以通过接口来实现

```java
interface Fly{
    public void fly();
}
//SuperMan是一个人，有飞行的能力。
class SuperMan extends People implements Fly{
    @Override
    public void fly(){
    }
}
```

一个类只能继承(extends)一个父类，但是可以实现(implements)多个接口。对于类来说接口是一种能力，一种规定。接口中只有方法的定义，没有具体实现，具体实现需要在实现类中自己实现。



由于Object是所有对象的最上层父类，所以都拥有它的一些方法

- equals() 用来比较对象是否相等，在Object类中是由==实现的，即比较两个对象地址是否相等，在String类中被重写成判断字符串中内容是否相等。一些场合下可以根据需求重写equals方法，但是如果在HashMap中用来作为key则需要更加彻底的重写HashCode()方法。
- hashCode() 返回一串hash code代表对象在内存中的地址，用来表示对象的地址看源码的时候发现只有一个方法的声明，没有具体实现，原来是使用native关键字调用的非java代码方法。
- notify()和notifyAll() 唤醒等待中的线程，第一个是唤醒单个，第二个是唤醒所有等待这个对象的monitor的线程。
- toString() 打印对象名+16进制的代表对象地址的hashCode。



可以用 instanceof来判断对象是否是某个类型或者属于他的子类型的对象。如果是则返回true，否则为false。
例：

```java
if(obj instanceof Object)
```

> 注：程序中类关系结构越复杂，性能越低下。
>
> 如果在子类的构造函数中显示调用父类的构造函数super()则必须是在子类构造函数的第一行。
>
> super不是一个指向对象的引用，只是一个特殊的关键字，告诉编译器需要调用父类
>
> super和this都不能用在 static块中。原因是类初始化的顺序为:
>  父类>子类>静态属性>静态代码块>静态方法>普通属性>普通方法

### 多态

同一个实现接口，使用不同的实例执行不同的操作。

多态分为运行时多态（方法的重写）以及编译时多态（方法的重载）。编译时多态指的是在编译时根据参数类型进行调用对应的方法，生成对应代码。运行时多态则在运行时取决于方法的调用对象来进行动态调用方法。

表现方式：
使用父类的引用，调用子类的对象。或者接口引用实现类的对象

体现：
父类（接口）统一管理行为，在方法中不注重实例的具体行为，直接调用父类的统一行为，由重写来调用实现对象的多态。

> 父类中的static修饰的方法不能被覆盖。

例：

```java
interface IA{
	int num=0;
	void say();
}
abstract class Base{
	int num=0;
	abstract void say();
}
class A extends Base{
	int num=1;
	void say(){
		System.out.println("in A class");
	}
}

class B extends Base{
	int num=2;
	void say(){
		System.out.println("in B class");
	}
}
class ImpIA1 implements IA{
	int num=1;
	@Override
	public void say() {
		System.out.println("Imp111");
	}
}
class ImpIA2 implements IA{
	int num=2;
	@Override
	public void say() {
		System.out.println("Imp222");
	}
}

public class TestPlantForm {
	public static void main(String[] args) {
		//接口方式
		runImp(new ImpIA1());
		runImp(new ImpIA2());
		//继承类方式
		runClass(new A());
		runClass(new B());
	}
	
	public static void runImp(IA ia){
		ia.say();
		System.out.println(ia.num);
	}
	public static void runClass(Base base){
		base.say();
		System.out.println(base.num);
	}
}
```

动态多态是对于方法的概念，对于属性并不使用，如果运行上面的例子，会发现输出的num值都为父类或者接口中的属性值。

> 在重写父类方法时需要注意
>
> - 子类中的访问修饰符权限要大于等于父类中的权限。
> - 重写方法的返回值可以是父类方法返回值的子类（或者实现的接口的实现类）
>
> 重写和重载区别：
>
> - 重载不覆盖重载对象的方法，函数名需要相同，返回值可以不同，参数列表需要不同。调用时根据参数调用相应方法
> - 重写需要方法名相同，参数名和返回值也相同或者关系为父子类或者接口与实现类的关系，会覆盖父类方法。调用时根据调用的对象进行调用。