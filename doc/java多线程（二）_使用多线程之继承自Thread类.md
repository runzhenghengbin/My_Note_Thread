> 一个进程正在运行时，至少拥有一个线程，java中也存在

### main线程

```java
package test;

public class Test {
  public static void main(String[] args) {
    //打印当前运行线程的名称
    System.out.println(Thread.currentThread().getName());
    //执行结果
    // main
  }

}
```

- 名称为main的线程执行mian函数中的代码

### 实现多线程方式

- 实现多线程的方式主要有2种
    - 继承自Thread类；
    - 实现自Runnable接口

#### 继承Thread类

> 继承自Thraed类，重写父类的run方法

```
package mythread;

public class MyThread extends Thread {
  @Override
  public void run() {
    for (int i = 0; i < 3; i++) {
      System.out.println(Thread.currentThread().getName());
    }
  }

  public static void main(String[] args) {
    MyThread myThread = new MyThread();
    myThread.start();
    for (int i = 0; i < 3; i++) {
      System.out.println(Thread.currentThread().getName());
    }
  }

}
```

- 执行结果

```
main
main
main
Thread-0
Thread-0
Thread-0
```
#### 总结
##### 1.如何在自定义的代码中，自定义一个线程呢？
创建线程的第一种方式：继承Thread类。
- 步骤：
    - 定义类继承Thread。
    - 复写Thread类中的run方法。
	    - 目的：将自定义代码存储在run方法。让线程运行。
    - 调用线程的start方法，
	    - 该方法两个作用：启动线程，调用run方法。

##### 2.发现运行结果每一次都不同?
- 因为多个线程都获取cpu的执行权。
- cpu执行到谁，谁就运行。明确一点，在某一个时刻，只能有一个程序在运行。(多核除外)
- cpu在做着快速的切换，以达到看上去是同时运行的效果。
我们可以形象把多线程的运行行为在互相抢夺cpu的执行权。

- 这就是多线程的一个特性：随机性。谁抢到谁执行，至于执行多长，cpu说的算。



##### 3.为什么要覆盖run方法呢？

- Thread类用于描述线程。
- 该类就定义了一个功能，用于存储线程要运行的代码。该存储功能就是run方法。
- wei也就是说Thread类中的run方法，用于存储线程要运行的代码。

##### 4.Thead类中start()方法和run()方法的区别 
- start()用来启动一个线程，当调用start()方法时，系统才会开启一个线程，通过Thead类中start()方法来启动的线程处于就绪状态（可运行状态），此时并没有运行，一旦得到CPU时间片，就自动开始执行run()方法。此时不需要等待run()方法执行完也可以继续执行下面的代码，所以也由此看出run()方法并没有实现多线程。 

- run()方法是在本线程里的，只是线程里的一个函数,而不是多线程的。如果直接调用run(),其实就相当于是调用了一个普通函数而已，直接待用run()方法必须等待run()方法执行完毕才能执行下面的代码，所以执行路径还是只有一条，根本就没有线程的特征，所以在多线程执行时要使用start()方法而不是run()方法。