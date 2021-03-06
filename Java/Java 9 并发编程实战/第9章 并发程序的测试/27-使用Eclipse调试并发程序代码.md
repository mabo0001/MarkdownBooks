### 9.9　使用Eclipse调试并发程序代码

如今，无论是哪种语言的开发者，都用IDE创建应用程序。在IDE内部通常都集成了许多功能特性，比如：

+ 项目工程管理；
+ 代码自动化生成；
+ 文档自动化生成；
+ 版本控制系统集成；
+ 应用程序调试器；
+ 用不同向导来创建应用程序的项目和元素。

其中调试器是IDE提供的一项非常有用的功能。在调试器的帮助下，你可以一步一步地执行应用程序，并分析程序的所有对象和变量值。

如果你用的是Java，那么Eclipse是最受欢迎的IDE之一。它内置了一款调试器，这个调试器可以帮助开发者进行测试。默认情况下，当调试并发应用程序或调试器发现断点时，它仅暂停有断点的线程，而允许其他线程继续执行。本节将介绍如何更改此配置，以帮助测试并发应用程序。

