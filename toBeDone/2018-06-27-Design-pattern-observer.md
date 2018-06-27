高级组件不应该以来低级组件的实现，而应该以来低级组件的接口或基类。

```java
interface IProgress{
	void doProgress(float progressVal);
}

class FileSpliter{
	String fileNum;
	String filePath;
	
	IProgress progress;

	public  FileSplitter(String fileNum,String filePath,IProgress progress){
		//读取文件

		//分批此向小文件写入
		for(int i=0;i<fileNum;i++){
			float progressVal=fileNum;
			progressVal=(i+1)/progressVal;
			progress.doProgress(progressVal);//更新进度条
		}
	}
}

```

观察者模式:一个对象发生改变，多个依赖的对象都收到通知。

```java
interface IProgress{
	void doProgress(float progressVal);
}

class FileSpliter{
	String fileNum;
	String filePath;
	
	List<IProgress> progressList;

	public  FileSplitter(String fileNum,String filePath){
		//读取文件

		//分批此向小文件写入
		for(int i=0;i<fileNum;i++){
			//....

			float progressVal=fileNum;
			progressVal=(i+1)/progressVal;
			onProgress(progressVal)
		}
	}

	public void addProgress(IProgress pro){
		progressList.add(pro);
	}

	public void removeProgress(IProgress pro){
		progressList.remove(pro);
	}

	public void onProgress(float val){
		循环调用doProgress
		for(){
			progress.doProgress(val);//更新进度条
		}
	}
}

```

定义:对象一对多的依赖关系，以便当一个对象状态发生改变时，所有依赖于它的对象都得到通知，并得到更新。
