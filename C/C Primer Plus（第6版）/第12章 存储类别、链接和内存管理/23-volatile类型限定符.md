#### 12.5.2　 `volatile` 类型限定符

`volatile` 限定符告知计算机，代理（而不是变量所在的程序）可以改变该变量的值。通常，它被用于硬件地址以及在其他程序或同时运行的线程中共享数据。例如，一个地址上可能存储着当前的时钟时间，无论程序做什么，地址上的值都随时间的变化而改变。或者一个地址用于接受另一台计算机传入的信息。

`volatile` 的语法和 `const` 一样：

```c
volatile int loc1;      /* loc1 是一个易变的位置 */
volatile int * ploc;    /* ploc 是一个指向易变的位置的指针 */
```

以上代码把 `loc1` 声明为 `volatile` 变量，把 `ploc` 声明为指向 `volatile` 变量的指针。

读者可能认为 `volatile` 是个可有可无的概念，为何ANSI委员把 `volatile` 关键字放入标准？原因是它涉及编译器的优化。例如，假设有下面的代码：

```c
val1 = x;
/* 一些不使用 x 的代码*/
val2 = x;
```

智能的（进行优化的）编译器会注意到以上代码使用了两次 `x` ，但并未改变它的值。于是编译器把 `x` 的值临时存储在寄存器中，然后在 `val2` 需要使用 `x` 时，才从寄存器中（而不是从原始内存位置上）读取 `x` 的值，以节约时间。这个过程被称为高速缓存（caching）。通常，高速缓存是个不错的优化方案，但是如果一些其他代理在以上两条语句之间改变了 `x` 的值，就不能这样优化了。如果没有 `volatile` 关键字，编译器就不知道这种事情是否会发生。因此，为安全起见，编译器不会进行高速缓存。这是在ANSI之前的情况。现在，如果声明中没有 `volatile` 关键字，编译器会假定变量的值在使用过程中不变，然后再尝试优化代码。

可以同时用 `const` 和 `volatile` 限定一个值。例如，通常用 `const` 把硬件时钟设置为程序不能更改的变量，但是可以通过代理改变，这时用 `volatile` 。只能在声明中同时使用这两个限定符，它们的顺序不重要，如下所示：

```c
volatile const int loc;
const volatile int * ploc;
```

