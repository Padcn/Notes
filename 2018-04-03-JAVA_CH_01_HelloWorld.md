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
		举例:(jdk安装路径为d:/jdk)则环境变量设置如下:
		JAVA_HOME=d:\jdk
		CLASSPATH=d:\jdk\lib
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
java HelloWorld
运行写好的HelloWorld屏幕上打印出了HelloWorld。
## 概念
