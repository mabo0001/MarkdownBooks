### 8.2　自定义ThreadPoolExecutor类

`Executor` 框架是一个允许线程的创建与执行分离的机制。而基于 `Executor` 和 `Executor Service` 接口的 `ThreadPoolExecutor` 类则实现了这两个接口。它有一个内置的线程池，提供了一些方法来允许传递两种类型的任务且由线程池中的线程来执行它们。这些任务是：

+ 实现 `Runnable` 接口的任务，它不会返回一个结果值；
+ 实现 `Callable` 接口的任务，它会返回一个结果值。

无论何种情况，只需传递任务到执行器即可。该执行器使用线程池中的一条线程或直接新建一个线程来执行这些任务。它也可以决定在何时去执行任务。

本节将介绍如何重写某些 `ThreadPoolExecutor` 类的方法，计算在执行器中执行任务的运行时间；当它完成执行以后，在控制台打印执行器的相关统计信息。

