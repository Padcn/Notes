适用于在类内游大量算法，例子
```java
enum TAX{
	CN_TAX,
	US_TAX,
	JP_TAX
}
class Test{
	public void calctax(TAX tax){
		if(tax==CN_TAX){
		....
		}
		if(tax==CN_TAX){
		....
		}
		...
	}
}
```

```java
abstract Tax{
	public String calctax();
}

class CnTax extends Tax{
	@Override
	public String calctax(){
		...
	}
}
class UsTax extends Tax{
	@Override
	public String calctax(){
		...
	}
}
class Test{
	public static void main(String args[]){
		Tax t=new CnTax();
		System.out.print(Test.calc(t));
	}
	public static String calc(Tax tax){
		return tax.calctax();
	}
}
```
靠多态调用来实现策略模式

模式定义
定义一系列算法，把他们一个个封装起来，并且使得他们可以互相替换(变化)。该模式使得算法可独立于使用他的客户程序(稳定)而变化(扩展，子类化).

Strategy及其子类为组建提供了一系列可重用的算法，从而可以使得类型在运行时方便的根据需要在各个算法之间进行切换。

Strategy模式提供了用条件判断语句以外的另一种选择，消除条件判断语句，就是在解耦合。含有许多条件判断语句的代码通常需要Strategy模式

如果Strategy对象没有实例变量，那么各个上下文可以共享同一个Strategy对象，从而节省对象开销.
