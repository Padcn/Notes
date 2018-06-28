在某些情况下

装饰器模式典型的就是IO，InputStream  FileInputStream


```java
abstract class Stream{
	void read();
	void write();
}

class FileStream extends Stream{
	Stream stream;
	//省略空构造

	public FileStream(Stream stream){
		this.stream=stream;
	}

	public void doSomething(){
		//....
		stream.read();
	}
}

class BufferStream extends Stream{
	Stream stream;

	//省略空构造

	public BufferStream(Stream stream){
		this.stream=stream;
	}

	public void doSomething(){
		//....
		stream.read();
	}
}

class Test{

	public static void main(String args[]){
		FileStream fs=new FileStream();
		BufferStream bs=new BufferStream(fs);
	}
}
```


```java
abstract class Stream{
	void read();
	void write();
}

abstract class DecortaorStream extends Stream{
	Stream stream;
}

class FileStream extends DecoratorStream{

	public FileStream(Stream stream){
		DecoratorStream(stream);
	}

	public void doSomething(){
		//....
		stream.read();
	}
}

class BufferStream extends DecoratorStream{

	public BufferStream(Stream stream){
		DecoratorStream(stream);
	}

	public void doSomething(){
		//....
		stream.read();
	}
}

class Test{

	public static void main(String args[]){
		FileStream fs=new FileStream();
		BufferStream bs=new BufferStream(fs);
	}
}
```

使用组合的方式使用多态。

动态(组合)地给一个对象增加一些额外的职责，就增加功能而言,Decorator模式比生成子类(继承)更为灵活(消除重复代码&减少子类个数)

通过采用组合而非继承的手法,Decorator模式实现了在运行时动态扩展对象的能力，而且可以根据需要扩展多个功能避免了继承带来的灵活性差和多子类衍生问题。

Decorator类在接口上表现为is-a Component的继承关系,即Decorator类继承了Component类具有的接口。但在实现上又表现为has-a Component的组合关系,即Decorator类又使用了另外一个Component类。

Decorator模式的目的并非解决多子类衍生的多继承问题，Decorator模式应用的要点在于解决主题类在多方向上的扩展功能——是为装饰的含义.



