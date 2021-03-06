### 8.4.1　Writer和Reader接口

`io` 包是围绕着实现了 `io.Writer` 和 `io.Reader` 接口类型的值而构建的。由于 `io.Writer` 和 `io.Reader` 提供了足够的抽象，这些 `io` 包里的函数和方法并不知道数据的类型，也不知道这些数据在物理上是如何读和写的。让我们先来看一下 `io.Writer` 接口的声明，如代码清单8-33所示。

代码清单8-33　 `io.Writer` 接口的声明

```go
type Writer interface {
　　Write(p []byte) (n int, err error)
}
```

代码清单8-33展示了 `io.Writer` 接口的声明。这个接口声明了唯一一个方法 `Write` ，这个方法接受一个 `byte` 切片，并返回两个值。第一个值是写入的字节数，第二个值是 `error` 错误值。代码清单8-34给出的是实现这个方法的一些规则。

代码清单8-34　 `io.Writer` 接口的文档

```go
Write从p里向底层的数据流写入len(p)字节的数据。这个方法返回从p里写出的字节
数（0 <= n <= len(p)），以及任何可能导致写入提前结束的错误。Write在返回n 
< len(p)的时候，必须返回某个非nil值的error。Write绝不能改写切片里的数据，
哪怕是临时修改也不行。
```

代码清单8-34中的规则来自标准库。这些规则意味着 `Write` 方法的实现需要试图写入被传入的 `byte` 切片里的所有数据。但是，如果无法全部写入，那么该方法就一定会返回一个错误。返回的写入字节数可能会小于 `byte` 切片的长度，但不会出现大于的情况。最后，不管什么情况，都不能修改 `byte` 切片里的数据。

让我们看一下 `Reader` 接口的声明，如代码清单8-35所示。

代码清单8-35　 `io.Reader` 接口的声明

```go
type Reader interface {
　　Read(p []byte) (n int, err error)
}
```

代码清单8-35中的 `io.Reader` 接口声明了一个方法 `Read` ，这个方法接受一个 `byte` 切片，并返回两个值。第一个值是读入的字节数，第二个值是 `error` 错误值。代码清单8-36给出的是实现这个方法的一些规则。

代码清单8-36　 `io.Reader` 接口的文档

```go
(1) Read最多读入len(p)字节，保存到p。这个方法返回读入的字节数（0 <= n 
<= len(p)）和任何读取时发生的错误。即便Read返回的n < len(p)，方法也可
能使用所有p的空间存储临时数据。如果数据可以读取，但是字节长度不足len(p)，
习惯上Read会立刻返回可用的数据，而不等待更多的数据。
(2) 当成功读取 n > 0字节后，如果遇到错误或者文件读取完成，Read方法会返回
读入的字节数。方法可能会在本次调用返回一个非nil的错误，或者在下一次调用时返
回错误（同时n == 0）。这种情况的一个例子是，在输入的流结束时，Read会返回
非零的读取字节数，可能会返回err == EOF，也可能会返回err == nil。无论如何，
下一次调用Read应该返回0, EOF。
(3) 调用者在返回的n > 0时，总应该先处理读入的数据，再处理错误err。这样才
能正确操作读取一部分字节后发生的I/O错误。EOF也要这样处理。
(4) Read的实现不鼓励返回0个读取字节的同时，返回nil值的错误。调用者需要将
这种返回状态视为没有做任何操作，而不是遇到读取结束。
```

标准库里列出了实现 `Read` 方法的4条规则。第一条规则表明，该实现需要试图读取数据来填满被传入的 `byte` 切片。允许出现读取的字节数小于 `byte` 切片的长度，并且如果在读取时已经读到数据但是数据不足以填满 `byte` 切片时，不应该等待新数据，而是要直接返回已读数据。

第二条规则提供了应该如何处理达到文件末尾（ `EOF` ）的情况的指导。当读到最后一个字节时，可以有两种选择。一种是 `Read` 返回最终读到的字节数，并且返回 `EOF` 作为错误值，另一种是返回最终读到的字节数，并返回 `nil` 作为错误值。在后一种情况下，下一次读取的时候，由于没有更多的数据可供读取，需要返回0作为读到的字节数，以及 `EOF` 作为错误值。

第三条规则是给调用 `Read` 的人的建议。任何时候 `Read` 返回了读取的字节数，都应该优先处理这些读取到的字节，再去检查EOF错误值或者其他错误值。最终，第四条约束建议 `Read` 方法的实现永远不要返回0个读取字节的同时返回 `nil` 作为错误值。如果没有读到值， `Read` 应该总是返回一个错误。

现在知道了 `io.Writer` 和 `io.Reader` 接口是什么样子的，以及期盼的行为是什么，让我们看一下如何在程序里使用这些接口以及 `io` 包。

