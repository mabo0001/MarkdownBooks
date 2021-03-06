### 2.10.3　poll()和select()的区别

虽然poll()和select()完成相同的工作，但poll()调用在很多方面仍然优于select()调用：

+ poll()不需要用户计算最大文件描述符值加1作为参数传递给它。
+ poll()对于值很大的文件描述符，效率更高。试想一下，要通过select()监视一个值为900的文件描述符，内核需要检查每个集合中的每个位，一直检查900个位。
+ select()的文件描述符集合是静态的，需要对大小设置进行权衡：如果值很小，会限制select()可监视的最大文件描述符值；如果值很大，效率会很低。当值很大时，大的位掩码操作效率不高，尤其是当无法确定集合是否稀疏集合。<a class="my_markdown" href="['#anchor27']"><sup class="my_markdown">[7]</sup></a>对于poll()，可以准确创建大小合适的数组。如果只需要监视一项，则仅传递一个结构体。
+ 对于select()调用，返回时会重新创建文件描述符集，因此每次调用都必须重新初始化。poll()系统调用会把输入（events变量）和输出（revents变量）分离开，支持无需改变数组就可以重新使用。
+ select()调用的timeout参数在返回时是未定义的。代码要支持可移植，需要重新对它初始化。而对于pselect()，不存在这些问题。

不过，select()系统调用也有些优点：

+ select()可移植性更好，因为有些UNIX系统不支持poll()。
+ select()提供了更高的超时精度：select()支持微秒级，poll()支持毫秒级。ppoll()和pselect()理论上都提供了纳秒级的超时精度，但是实际上，这两个调用的毫秒级精度都不可靠。

比起poll()调用和select()调用，epoll()调用更优，epoll()是Linux特有的I/O多路复用解决方案，我们将在第4章详细探讨。

