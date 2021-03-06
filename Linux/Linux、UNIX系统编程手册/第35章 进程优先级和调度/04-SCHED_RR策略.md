### 35.2.1　SCHED_RR策略

在SCHED_RR（循环）策略中，优先级相同的进程以循环时间分享的方式执行。进程每次使用CPU的时间为一个固定长度的时间片。一旦被调度执行之后，使用SCHED_RR策略的进程会保持对CPU的控制直到下列条件中的一个得到满足：

+ 达到时间片的终点了；
+ 自愿放弃CPU，这可能是由于执行了一个阻塞式系统调用或调用了sched_yield()系统调用（35.3.3节将予以介绍）；
+ 终止了；
+ 被一个优先级更高的进程抢占了。

对于上面列出的前两个事件，当运行在SCHED_RR策略下的进程丢掉CPU之后将会被放置在与其优先级级别对应的队列的队尾。在最后一种情况中，当优先级更高的进程执行结束之后，被抢占的进程会继续执行直到其时间片的剩余部分被消耗完（即被抢占的进程仍然位于与其优先级级别对应的队列的队头）。

在SCHED_RR和SCHED_FIFO两种策略中，当前运行的进程可能会因为下面某个原因而被抢占：

+ 之前被阻塞的高优先级进程解除阻塞了（如它所等待的I/O操作完成了）；
+ 另一个进程的优先级被提到了一个级别高于当前运行的进程的优先级的优先级；
+ 当前运行的进程的优先级被降低到低于其他可运行的进程的优先级了。

SCHED_RR策略与标准的循环时间分享调度算法（SCHED_OTHER）类似，即它也允许优先级相同的一组进程分享CPU时间。它们之间最重要的差别在于SCHED_RR策略存在严格的优先级级别，高优先级的进程总是优先于优先级较低的进程。而在SCHED_OTHER策略中，低nice值（即高优先级）的进程不会独占CPU，它仅仅在调度决策时为进程提供了一个较大的权重。前面35.1节中曾经讲过，一个优先级较低的进程（即高nice值）总是至少会用到一些CPU时间的。它们之间另一个重要的差别是SCHED_RR策略允许精确控制进程被调用的顺序。

