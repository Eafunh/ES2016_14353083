#Deadlock 死锁
####14M1 14353083 何裕丰
***
##什么是死锁？
何谓锁：是指两个或多个进程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象。

何谓死：若无采取适当措施改变某些条件，线程间将会一直处于互相等待状态，一直阻塞下去。

##产生死锁的四个必要条件

* 互斥条件：一个资源每次只能被一个进程使用。
* 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
* 不剥夺条件：进程已获得的资源，在末使用完之前，不能强行剥夺。
* 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

##如何避免死锁？
破化死锁产生的四个必要条件。

##死锁实验
``` 
class Deadlock implements Runnable {
    A a = new A();
	B b = new B();
	
	Deadlock(){
		Thread t = new Thread(this);
		int count = 20000;
		t.start(); //线程t开始
		while(count-->0); //空循环等待
		a.methodA(b);
	}
	
	@Override
	public void run() {
		// TODO Auto-generated method stub
		b.methodB(a);
	}
	public static void main(String args[]){
		new Deadlock();
	}
	
}
```
```
class A {
    synchronized void methodA(B b){
		b.last();
	}
	synchronized void last(){
		System.out .println("Inside A.last()");
	}
}
```
```
class B{
    synchronized void methodB(A a){
		a.last();
	}
	synchronized void last(){
		System.out .println("Inside B.last()");
	}
}
```
用eclipse运行上面的java代码，并在产生的class文件所在目录添加bat文件：
```
cd/d %~dp0
@echo off
:start
set/a var+=1
echo %var%
java Deadlock
if %var% leq 1000 GOTO start
pause
```
双击运行：

![Result](http://i1.piimg.com/4851/2ce9817ac3315cd3.png)

跑了7次产生死锁，停了下来。
##结果分析
1. 程序main函数首先创建了一个Deadlock的实例。
2. 该实例初始化分别创建A、B的实例a、b，调用构造函数。
3. 在构造函数中创建t线程，插入到调度队列中。
4. 当t开始被调度时，执行run()函数,由b执行methodB(A a)，再调用A.last()输出，由于methodB和last函数均为synchronized类型，所以他们在同一时刻最多只有一个线程可执行，相当于被占有。此时b占有B.methodB()，再进而去占有A.last()。
5. while循环过后，a执行methodA()，同理a占有A.methodA()，再进而去占有B.last()。
6. 利用批处理文件让程序不停地跑，当跑到一定的次数，由于前面程序的线程还没来得及结束、释放，对代码块仍处于访问状态，即仍在占有，此时新程序又正在等待资源。如：由于synchronized修饰的函数只能被一个线程访问，其他访问线程将被阻塞（互斥条件），前面的线程执行a.mmethodA锁住了A，methodA中又等待B，而后面的线程执行methodB锁住了B，methodB中等待A（请求与保持条件），他们在完成任务之前都不会释放资源（不剥夺条件），因此陷入了循环等待状态，从而产生死锁。

##实验感想
 之前操作系统理论和实验课都已经强调过很多次死锁的问题，这次实验用一个小小的例子让我们再一次回顾并加深了对死锁的理解。死锁实际上就是线程j之间关于资源等待、占有的一个死循环，理解时可以用需求和供求来类比理解，而避免死锁，也只要打破他们之间的供需不平衡的关系即可。
