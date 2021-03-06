### 31.3.2　线程特有数据API概述

要使用线程特有数据，库函数执行的一般步骤如下。

**1．** 函数创建一个键（key），用以将不同函数使用的线程特有数据项区分开来。调用函数pthread_key_create()可创建此“键”，且只需在首个调用该函数的线程中创建一次，函数pthread_once()的使用正是出于这一目的。键在创建时并未分配任何线程特有数据块。

**2．** 调用pthread_key_create()还有另一个目的，即允许调用者指定一个自定义解构函数，用于释放为该键所分配的各个存储块（参见下一步）。当使用线程特有数据的线程终止时，Pthreads API会自动调用此解构函数，同时将该线程的数据块指针作为参数传入。

**3．** 函数会为每个调用者线程创建线程特有数据块。这一分配通过调用malloc()（或类似函数）完成，每个线程只分配一次，且只会在线程初次调用此函数时分配。

**4．** 为了保存上一步所分配存储块的地址，函数会使用两个Pthreads函数：pthread_setspecific()和pthread_getspecific()。调用函数pthread_setspecific()实际上是对Pthreads实现发起这样的请求：保存该指针，并记录其与特定键（该函数的键）以及特定线程（调用者线程）的关联性。调用pthread_getspecific()所执行的是互补操作：返回之前所保存的、与给定键以及调用线程相关联的指针。如果还没有指针与特定的键及线程相关联，那么pthread_getspecific()返回NULL。函数可以利用这一点来判断自身是否是初次为某个线程所调用，若为初次，则必须为该线程分配空间。

