## 线程

### 概述  

> 进程：在当前操作系统中正在运行的应用程序。
>
> 线程：在一个程序中正在运行的功能，如果在同一时刻执行多个功能的情况下，就称之为多线程操作。
> <font color=yellow>在Java中必须存在一个线程，该线程叫做main线程也称之为主线程</font>。通过程序定义出线程实现子线程操作，体现Java中的多线程操作。
>
> CPU：在多线程编程中，每个线程需要被执行必须由CPU分配资源才能获取到执行权利。<font color=red>程序无法控制CPU资源分配。</font> 

### 划分点

* Thread类
* Runnable接口
* 线程同步和生命周期
* 生产者&消费者模式
* 线程池

> * ####  Thread类 
>
> > java.lang包，该类提供了Java多线程编程的功能操作，同时每定义一个Thread对象表示在Java中诞生一个线程。如果需要在程序中指定除自定义的线程只需要继承Thread重写run方法添加自定义功能。
> >
> > **线程声明：** 
> >
> > ``` java
> >//原型
> > public class MyThread extends Thread(){
> >  @Override
> > 	public void run() {
> >     	for(int i=0;i<3;i++){
> >          System.out.println("MyThread"+i);
> >         }
> >     }
> >    }
> >    ```
> > 
> > **线程方法：** 
> >
> > 1. start方法	-启动线程，在该方法中会自动调用run方法。
> >
> >    ``` java
> >     MyThread mt=new MyThread();
> >    mt.start();
> >    ```
> > 
> >    
> >
> > 2. sleep方法  -线程休眠，通过指定的时间控制线程的休眠操作，一旦线程进入休眠后，在恢复执行之前cpu会将当前线程纳入队列等待过程中，<font color=red>main函数主线程不能sleep()</font>。
> >
> >    ``` java
> >     @Override
> >    public void run() {
> >        for(int i=0;i<3;i++){
> >            System.out.println("MyThread"+i);
> >            try {
> >                sleep(500);	//线程休眠
> >            } catch (InterruptedException e) {
> >                e.printStackTrace();
> >            }
> >        }
> >    }
> >    ```
> > 
> >    
> >
> > 3. stop方法    <font color=grey>-过时方法</font> 
> >
> > 4. interrupt方法  -线程中断，如果程序中存在正在执行的线程通过中断操作，会将线程带入阻塞状态，进入该状态的线程可以通过CPU程序分配资源进行启动，但也会直接终止。
> >
> > 5. join方法     -等待，将当前CPU资源让出让线程执行完毕后才执行后续的线程
> >
> > 6. 其余方法：wait等待   notify唤醒      <font color=yellow>属于Object类中的方法，针对于线程实现控制的一系列方法。</font> 
> >
> >    <font color=green>这两个方法实现了多线程编程中设计模式（生产者，消费者），体现了Java程序中高内聚低耦合的效果。</font> 
>
> ---
>
> * #### 接口：Runnable
>
> > 该接口属于线程的功能接口，通常情况所有线程功能不会直接通过Thread类方式编写，因为Thread类行为无法实现线程资源的共享。
> >
> > ``` java
> > //定义线程功能对象
> > MyRunnable mr=new MyRunnable();
> > //创建线程对象
> > Thread thead1=new Thread(mr);
> > Thread thead2=new Thread(mr);
> > 
> > ```
> >
> > 
> >
>
> * #### 线程同步和生命周期
>
> > **线程同步：** 
> > 在线程操作中CPU在分配资源有对拥有资源的线程进行保护操作，防止其他线程进行资源的抢占行为，并且被保护的资源会通过锁的机制对被同步的线程进行控制，但在锁操作中尽量避免死锁现象。
> >
> > 类型：
> >
> >  1. 同步代码块
> >
> >     ``` java
> >     synchronized(对象){
> >         //同步处理线程功能代码
> >     }
> >     ```
> >
> >     
> >
> >  2. 同步方法
> >
> >     ``` java
> >     public synchronized void test(){
> >         //同步方法功能代码
> >     }
> >     ```
> >
> > **生命周期：** 
> >        新建、就绪、运行、阻塞(中断)、死亡
> >
> > ---
> * #### 生产者&消费者模式
> >在多线程中因为模式中会存在缓冲区，而<font color=yellow>生产者&消费者模式不存在缓冲区，因为生产者和消费者没有直接的依赖，耦合度比较低。</font> 
> >
> ><font color=red>**耦合：（包含：耦合性、内聚性）**</font> 
> >
> >1. 耦合性
> >
> >所包含的就是块间联系，<font color=yellow>方法和方法之间的联系叫快间联系。</font> 
> >
> >2. 内聚性
> >
> >所包含的就是块内联系，<font color=yellow>方法内的功能与功能之间的联系。</font> 
> >
> ><font color=red>在程序中所编写的所有功能必须实现解耦操作，提高功能之间的依赖关系，最终达到低耦合高内聚的现象。</font> 
> >
> ><font color=red>**高并发：**</font> 
> ><font color=yellow>通过缓存区进行数据的处理提高程序效率，也可以规避线程的阻塞问题。</font>
> >Java多线程中会使用线程池来实现缓冲区的操作从而优化所有线程。
> >
> ><font color=red>生产者&消费者模式案例：</font> 
> >
> >**Computer类：** 
> >
> >``` java
> >public class Computer {
> >	//电脑数量属性
> >	private int number;	
> >	//电脑生产方法
> >	public synchronized void product() throws InterruptedException {
> >		//循环生产 电脑
> >		while(number!=0) {
> >			//将当前生产者实现等待操作
> >			this.wait();
> >		}
> >		System.out.println("生产电脑");
> >		//唤醒生产者者
> >		this.notify();
> >		number++;
> >	}
> >	//消费电脑方法
> >	public synchronized void consumer() throws InterruptedException {
> >		while(number==0) {
> >			//当产品没有时需要等待生产者生产
> >			this.wait();
> >		}
> >		System.out.println("消费电脑");
> >		//唤醒消费者
> >		this.notify();
> >		number--;
> >	}
> >}
> >```
> >
> >**生产者&消费者线程：** 
> >
> >``` java
> >public class ProductRunnable implements Runnable {
> >	Computer cp;	//电脑属性
> >	public ProductRunnable(Computer cp) {
> >		this.cp=cp;
> >	}
> >	@Override
> >	public void run() {
> >		while(true) {
> >			try {
> >                //执行生产者功能
> >				cp.product();
> >				Thread.sleep(1000);
> >			} catch (InterruptedException e) {
> >				e.printStackTrace();
> >			}
> >		}
> >	}
> >
> >}
> >
> >public class ConsumerRunnable implements Runnable {
> >	Computer cp;	//电脑属性
> >	public ConsumerRunnable(Computer cp) {
> >		this.cp=cp;
> >	}
> >	@Override
> >	public void run() {
> >		while(true) {
> >			try {
> >                //执行消费者功能
> >				cp.consumer();
> >				Thread.sleep(1000);
> >			} catch (InterruptedException e) {
> >				e.printStackTrace();
> >			}
> >		}
> >	}
> >
> >}
> >```
> >
> >**测试类：** 
> >
> >``` java
> >public class Test {
> >
> >	public static void main(String[] args) {
> >		Computer cp=new Computer();
> >		
> >		ProductRunnable pr=new ProductRunnable(cp);
> >		ConsumerRunnable cr=new ConsumerRunnable(cp);
> >		new Thread(pr).start();
> >		new Thread(cr).start();
> >		
> >	}
> >}
> >```
> >
> >
>
> ---
> * #### 线程池
>
> > API：Executors、ExecutorsService
> >
> > CachedThreadPool

<font color=red></font>
<font color=yellow></font>
<font color=green></font>