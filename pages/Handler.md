- ## Looper
	- 安卓是事件驱动的，所有事件都是loop启动的
	- App 启动时，会调用到 ActivityThread 中，Looper 就在其 main() 方法中被启动；main() 中会主动调用 Looper.prepareMainLooper() 和 Looper.loop()
	-
##### Handler原理

两种使用方法：

post方法

创建内部Handler类，在执行new Handler时，Handler默认情况下会绑定当前代码执行的主线程，当我们在自创子线程完成操作后，将需要发送的消息内容包裹在runnable中通过Handler的post方法发送Messagequeue(最后runnable仍然会被封装为message), 然后经过Looper的循环将其交给Handler进行处理

sendMessage方法

handler创建内部类，重写handleMessage进行消息处理，同样的在子线程进行相应处理，用sendMessage将消息传入MessageQueue队列，传递的是Message类，Message 中的int类型what，用当做Message的标识符。中的其他两个int类型arg1，arg2,还有一个object类型的obj,以及setData，getData方法用处理Bundle(键值对类型)对象
##### Message的创建方法

obtains(这样会复用之前的Message的内存，不会频繁的创建对象),直接new
-
##### Handler过程

handler有两个作用，能够发送消息和处理Looper分发给他的消息，handler是消息发送到指定MessageQueue，然后通过Looper将消息分发给Handler处理

Message ：代表一个行为what或者一串动作Runnable, 每一个消息在加入消息队列时,都有明确的目标Handler

ThreadLocal： 线程本地存储区（Thread Local Storage，简称为TLS），每个线程都有自己的私有的本地存储区域，不同线程之间彼此不能访问对方的TLS区域。ThreadLocal的作用是提供线程内的局部变量TLS,这种变量在线程的生命周期内起作用,每一个线程有他自己所属的值(线程隔离)

MessageQueue (C层与Java层都有实现) ：以队列的形式对外提供插入和删除的工作, 其内部结构是以双向链表的形式存储消息的,当没有消息时，此时主线程会释放CPU资源进入休眠状态，直到下个消息到达或者有事务发生

Looper (C层与Java层都有实现) ：Looper是循环的意思,它负责从消息队列中循环的取出消息然后把消息交给Handler处理

Handler ：消息的真正处理者, 具备获取消息、发送消息、处理消息、移除消息等功能
##### Hander原理

Handler 的 runWithScissors() 可以实现 A 线程向 B 线程发送一个消息，使 A 线程进入阻塞，等待 B 线程处理完消息后再继续执行
- ##### 主线程 Looper 何时运行？
  
  Tips：ActivityThread 不继承自 Thread，它只是一个运行在主线程上的对象；
##### 子线中开辟Looper?

子线程中Looper.prepare()创建Looper对象并且关联到线程，创建Handler对象，Looper.loop()开启循环
##### 既然可以存在多个Handler往MessageQueue中添加数据(发消息是各个handler可能处于不同线程)，那他内部是如何确保线程安全的？ 

在添加数据和执行next的时候都加了this锁，这样可以保证添加的位置是正确的，获取的也会是最前面的。
- ## 面试
	- ### 一个线程可以有几个Handler几个Looper?
		- 多个handler一个Looper
	- ##### Handler使用的什么什么设计模式？
	  
	  生产者消费者模式：Handler.sendMessage相当于一个生产者,MessageQueue相当于容器，Looper相当于消费者。