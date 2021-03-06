[toc]

### 4.5.1　Python多进程与GIL

要对Python线程和进程进行长期的性能检查，首先必须要了解全局解释器锁（GIL）。GIL是Python解释器使用的一种机制，同一时间只会有一个线程执行代码，也就意味着Python代码是线性执行的（即使使用多进程和多核）。该设计决定了Python可以运行得很快，但又是线程安全的。

> <img class="my_markdown" src="../images/35.jpg" style="zoom:50%;" />
> 如果你还没有看过PyCon 2010中David Beazley关于GIL理解的演讲，我推荐你看一下。Beazley还在他的博客上有很多文章，并且在GILectomy（试图从Python中移除GIL以实现快速的多进程）上有一些有趣的发言。

GIL在高I/O操作上增加了额外的性能负担，比如网络爬虫。有一些方式可以利用Python的多进程库更好地达到跨进程和线程的数据共享。

我们可以把爬虫写成一个带有工作池或队列的映射，来对比Python自身的多进程内部处理与基于Redis的系统。我们也可以使用异步编程，增强线程性能，提高网络利用率。类似async、tornado甚至NodeJS的异步库，可以让程序以非阻塞的方式执行，这就意味着进程可以在等待网络服务器响应时切换到不同的线程。这些实现方式很可能会比我们的用例速度更快。

另外，我们还可以使用类似PyPy的项目，帮助提升多线程和多进程的速度。也就是说，在实现优化之前，你需要测量性能并评估需求（不要过早优化）。时刻询问自己速度是否比清晰度更重要，直觉是否比实际观察更正确，这是一个很好的规则。请谨记Python之禅，然后继续前行吧！

