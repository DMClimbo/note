## 基础概念

- CISC：复杂指令集(x86)

- RISC：精简指令集(ARM)

- ARM：Advanced RISC machines

- POSIX：方便在Linux下运行的C API(对应open，文件不带缓冲)  

- ANSI：标准C API(对应fopen，采用文件流的形式，文件带缓冲)

  ​	
  
  

## 操作系统

操作系统是一类特殊的系统软件，管理整个系统的硬件和软件，是最接近硬件的软件，屏蔽硬件的底层设计向应用软件提供一个统一接口

​	

- 线性存储管理：所有存储器和外设安排到一个统一的地址空间，通过地址映射到不同设备，便于管理
- shell：linux命令行通过一种叫shell的程序使用系统提供的功能，shell负责接收用户的输入，解析输入的命令的参数，bash一般是默认的shell





## 运行编译

OS会使用exec()函数运行程序，在调用main()函数之前，exec()会先调用一个特殊的启动例程，负责从内核读取程序的命令行参数

> int main(int argc, char* argv[])
>
> - argc     表示argv有多少字符串
> - argv     不定长字符串数组

​		



## 进程线程

进程间通信方式：管道、FIFO、消息队列、信号量、共享内存和socket

- 共享内存：共享内存是在内存中开辟一段空间，供不同进程访问，共享内存不仅能在多个不同进程(非父子进程)间共享数据，而且可以比管道传输更大量的数据

  > #include <sys/ipc.h>
  >
  > #include<sys/shm.h>
  >
  > int shmget(key_t key, size_t size, int shmflg)       //创建共享内存，成功返回共享内存ID
  >
  > - key            由ftok函数生成的一个系统唯一的关键字，用来在系统中标识一块内存
  > - size           共享内存大小
  > - shmflg      内存操作方式

  ​			

  > void  *shmat(int shmid, const void *shmaddr,  int shmflg)      //获取共享内存ID对应的内存起始地址
  >
  > - shmid        共享内存ID
  > - shmaddr   指定共享内存地址，若为0表示让系统决定
  > - shmflg        内存操作方式

  ​		

  > int shmdt(const void* shmaddr)        //从程序中分离一块地址
  >
  > - shmaddr    要分离的共享内存地址