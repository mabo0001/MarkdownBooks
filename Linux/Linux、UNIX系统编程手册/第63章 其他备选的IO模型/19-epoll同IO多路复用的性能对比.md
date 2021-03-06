### 63.4.5　epoll同I/O多路复用的性能对比

表63-9展示了当我们使用poll()、select()以及epoll监视 0 到N−1的N个连续文件描述符时的结果（在2.6.25版内核上）。（该测试设定为在每次监视中，只有一个随机选择的文件描述符处于就绪态。）从这个表格中，我们发现随着被监视的文件描述符数量的上升，poll()和select()的性能表现越来越差。与之相反，当N增长到很大的值时，epoll的性能表现几乎不会降低。（当N值上升时，微小的性能下降可能是由于测试系统上的CPU cache达到了上限。）

<center class="my_markdown"><b class="my_markdown">表63-9：poll()、select()以及epoll进行100000次监视操作所花费的时间</b></center>

| 被监视的文件描述符数量（N） | poll()所占用的CPU时间（秒） | select()所占用的CPU时间（秒） | epoll所占用的CPU时间（秒） |
| :-----  | :-----  | :-----  | :-----  | :-----  | :-----  |
| 10 | 100 | 1000 | 10000 | 0.61 | 2.9 | 35 | 990 | 0.73 | 3.0 | 35 | 930 | 0.41 | 0.42 | 0.53 | 0.66 |

> 基于本测试的目的，我们在glibc的头文件中将FD_SETSIZE修改为 16384，以此允许测试程序在使用select()时能监视大量的文件描述符。

在63.2.5 节中我们知道了为什么 select()和 poll()在监视大量的文件描述符时性能表现很差。现在我们看看为什么epoll的性能表现会更好。

+ 每次调用select()和poll()时，内核必须检查所有在调用中指定的文件描述符。与之相反，当通过epoll_ctl()指定了需要监视的文件描述符时，内核会在与打开的文件描述上下文相关联的列表中记录该描述符。之后每当执行 I/O 操作使得文件描述符成为就绪态时，内核就在epoll描述符的就绪列表中添加一个元素。（单个打开的文件描述上下文中的一次I/O事件可能导致与之相关的多个文件描述符成为就绪态。）之后的epoll_wait()调用从就绪列表中简单地取出这些元素。
+ 每次调用 select()或 poll()时，我们传递一个标记了所有待监视的文件描述符的数据结构给内核，调用返回时，内核将所有标记为就绪态的文件描述符的数据结构再传回给我们。与之相反，在 epoll 中我们使用 epoll_ctl()在内核空间中建立一个数据结构，该数据结构会将待监视的文件描述符都记录下来。一旦这个数据结构建立完成，稍后每次调用 epoll_wait()时就不需要再传递任何与文件描述符有关的信息给内核了，而调用返回的信息中只包含那些已经处于就绪态的描述符。

> 除了以上几点外，对于select()来说，我们必须在每次调用之前先初始化输入数据。而无论是select()还是poll()，我们必须对返回的数据结构做检查，以此找出N个文件描述符中有哪些是处于就绪态的。但是，通过一些测试得出的结果表明，这些额外的步骤所花费的时间同系统调用监视N个文件描述符所花费的时间相比就显得微不足道了。表63-9并没有包含这些检查步骤所用的时间。

粗略来看，我们可以认为当N（被监视的文件描述符数量）取值很大时，select()和poll()的性能会随着N的增大而线性下降。这可以从表63-9中N=100和N=1000时的情况得到。而当N=10000时，性能伸缩性实际上比线性还要差。

与之相反的是，epoll的性能会根据发生I/O事件的数量而扩展（呈线性）。因此常见的能够高效使用epoll API的应用场景就是需要同时处理许多客户端的服务器：需要监视大量的文件描述符，但大部分处于空闲状态，只有少数文件描述符处于就绪态。

