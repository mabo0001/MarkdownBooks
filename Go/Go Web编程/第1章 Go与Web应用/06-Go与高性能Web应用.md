### 1.1.4　Go与高性能Web应用

高性能不仅意味着能够在短时间内处理大量请求，还意味着服务器能够快速地对客户端进行响应，并让终端用户（end user）能够快速地执行操作。

Go语言的一个设计目标就是提供接近于C语言的性能，尽管这个目标目前尚未达成，但Go语言现在的性能已经非常具有竞争力：Go程序会被编译为本地码（native code），这一般意味着Go程序可以运行得比解释型语言的程序要快，并且就像前面说过的那样，Go语言的goroutine对并发编程提供了非常好的支持，这使得Go应用可以同时处理多个请求。

希望以上介绍能够引起你对使用Go语言及其平台进行Web开发的兴趣。但是在学习如何使用Go进行Web开发之前，我们需要先来了解一下什么是Web应用，以及它们的工作原理是什么，这会给我们学习之后几章的内容带来非常大的帮助。

