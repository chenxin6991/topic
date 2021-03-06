#### 1.TCP的三次握手与四次挥手过程，各个状态名称与含义 ####

[https://www.cnblogs.com/zedosu/p/6710167.html](https://www.cnblogs.com/zedosu/p/6710167.html)
#### 2.new/delete和malloc/free的用法和区别 ####

1.malloc/free为C标准库函数，而new/delete为C++的操作符    
2.malloc开辟空间类型大小需要手动计算，new是由编译器自己计算     
3.malloc返回值类型为void*，必须强转为对应类型的指针，new则直接返回对应类型的指针     
4.malloc开辟内存时返回内存地址需要判空，失败返回NULL，而new则不需要判断，因为内存分配失败时，它会剖出异常bad_alloc    
5.malloc/free为函数只是开辟空间/释放空间，new/delete不仅会开辟空间，还会调用构造函数和析构函数进行初始化和清理    
6.new/delete底层是基于malloc/free来实现的，而malloc/free不能基于new/delete实现    
7.new/delete是操作符可以被重载，而malloc/free不行    
8.对于malloc分配内存后，若在使用过程中内存分配不够或太多，这时可以使用realloc函数对其进行扩充或缩小，但是new分配好的内存不能这样被直观简单的改变     
9.对于new/delete若内存分配失败，用户可以指定处理函数或重新制定分配器（new_handler(可以在此处进行扩展)），malloc/free用户是不可以处理     
10.对于new/delete与malloc/free申请内存位置说明，malloc我们知道它是在堆上分配内存的，但new其实不能说是在堆上，C++中，对new申请内存位置有一个抽象概念，它为自由存储区，它可以在堆上，也可以在静态存储区上分配，这主要取决于operator new实现细节，取决与它在哪里为对象分配空间   

#### 3.C++中struct和class的区别 ####
1.默认的访问权限，struct是public的，class是private的   
2.class这个关键字还可以用于定义模板参数，就像typename，而struct不用于定义模板参数  
3.C++中struct是对C中的struct的补充，兼容过去C中struct所以的特性   
#### 4.同步和异步、阻塞和非阻塞的区别 ####
同步、异步：  
概念：消息的通知机制  
解释：涉及到IO通知机制；所谓同步，就是发起调用后，被调用者处理消息，必须等处理完才直接返回结果，没处理完之前是不返回的，调用者主动等待结果；所谓异步，就是发起调用后，被调用者直接返回，但是并没有返回结果，等处理完消息后，通过状态、通知或者回调函数来通知调用者，调用者被动接收结果。  

阻塞、非阻塞：  
概念：程序等待调用结果时的状态  
解释：涉及到CPU线程调度；所谓阻塞，就是调用结果返回之前，该执行线程会被挂起，不释放CPU执行权，线程不能做其它事情，只能等待，只有等到调用结果返回了，才能接着往下执行；所谓非阻塞，就是在没有获取调用结果时，不是一直等待，线程可以往下执行，如果是同步的，通过轮询的方式检查有没有调用结果返回，如果是异步的，会通知回调。
#### 5.什么是临界区、临界资源、管理临界区的基本原则是什么？ ####
临界区：每个进程中访问临界资源的那段程序叫做临界区。进程对临界区的访问必须互斥，每次只允许一个进程进去临界区，其他进程等待。
  
临界资源：指每次只允许一个进程访问的资源，分硬件临界资源、软件临界资源。  

临界区管理的基本原则是：   
①如果有若干进程要求进入空闲的临界区，一次仅允许一个进程进入。  
②任何时候，处于临界区内的进程不可多于一个。如已有进程进入自己的临界区，则其它所有试图进入临界区的进程必须等待。  
③进入临界区的进程要在有限时间内退出，以便其它进程能及时进入自己的临界区。  
④如果进程不能进入自己的临界区，则应让出CPU，避免进程出现“忙等”现象。   
#### C++中const在函数名前面和函数后面的区别 ####
当const在函数名前面的时候修饰的是函数返回值，在函数名后面表示是常成员函数，该函数不能修改对象内的任何成员，只能发生读操作，不能发生写操作。  
