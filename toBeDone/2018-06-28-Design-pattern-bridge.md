桥模式

某些类型的固有逻辑，使得他们具有两个变化的维度，乃至多个维度的变化。

```java

abstract class Message{
	public MessageImp imp;

	public void sendMsg();
	public void showMsg();
}
abstract class MessageImp{
	public void connect();
	public void play();
}

public class PcMessageImp extends MessageImp{
	//根据不同实现
}
public class MobileMessageImp extends MessageImp{
	//根据不同实现
}

class PcMessage extends Message{
	//省略构造函数调用父类构造Imp
	public void sendMsg(){
		imp.connect();
		imp.play();
	}
	public void showMsg(){
		//调用imp...
	};
}
class MobileMessage extends Message{
	//省略构造函数调用父类构造Imp
	public void sendMsg(){
		imp.connect();
		imp.play();
	}
	public void showMsg(){
		//调用imp...
	};

}

class Test{

	public static void main(String args[]){
		MessageImp imp=new PcMessageImp();
		Message m=new MobileMessage(imp);
	}
}
```

Birdge模式使用 对象间的组合关系 解藕了抽象和实现之间固有的绑定关系，使得抽象和实现可以沿着各自的维度来变化。所谓抽象和实现沿着各维度的变化，即 子类化 他们

Bridge 模式有时候类似于多继承方案，但由于多继承方案往往违背单一职责原则 即一个类只有一个变化的原因 复用性较差。Bridge模式是比多继承更好的解决方法。

Bridge模式的应用一般在 两个非常强的变化维度，有时候一个类也游多于两个的比阿华维度，这时可以使用Bridge的扩展模式。
