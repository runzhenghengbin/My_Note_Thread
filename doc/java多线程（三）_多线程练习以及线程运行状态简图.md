> 现在就根据毕向东的视频教程进行一步一步书写文章

### 练习题1
```java

/*
练习：
创建两个线程，和主线程交替运行。

原来线程都有自己默认的名称。
Thread-编号 该编号从0开始。


static Thread currentThread():获取当前线程对象。
getName(): 获取线程名称。

设置线程名称：setName或者构造函数。

*/

public class ThreadDemo  extends Thread{
	
	ThreadDemo(String name){
		super(name);
	}
	@Override
	public void run() {
		for (int i = 0; i < 3; i++) {
			System.out.println(Thread.currentThread().getName()+" run..."+i);
		}
	}
	
	public static void main(String[] args) {
		ThreadDemo t1 = new ThreadDemo("one");
		ThreadDemo t2 = new ThreadDemo("two");
		t1.start();
		t2.start();
		for (int i = 0; i < 3; i++) {
			System.out.println(Thread.currentThread().getName()+" run..."+i);
		}
		
	}

}
```
- 执行结果
```
main run...0
one run...0
two run...0
two run...1
two run...2
one run...1
one run...2
main run...1
main run...2
```

### 线程状态

![image](http://p2dozdum2.bkt.clouddn.com/%E7%BA%BF%E7%A8%8B%E7%8A%B6%E6%80%81.png)

### 参考
- 毕向东java教学视频