### 第10章　不安全的Rust和外部函数接口

Rust是一种具有两种模式的语言：安全模式（默认）和不安全模式。在安全模式下，你可以获得各种安全特性使你免受严重错误的影响，但有时你需要摆脱编译器提供的安全特性，并额外获得其他方面的控制。一种用例与其他语言（例如C语言）进行交互，这可能非常不安全。在本章中，你将了解Rust必须与其他语言交互时需要做哪些额外的工作，以及如何使用不安全模式来促成和明确此交互。

在本章中，我们将介绍以下主题。

+ 安全模式和不安全模式。
+ Rust中的不安全操作。
+ 外部函数接口，以及与C语言交互。
+ 使用PyO3与Python交互。
+ 使用Neon与Node.js交互。

