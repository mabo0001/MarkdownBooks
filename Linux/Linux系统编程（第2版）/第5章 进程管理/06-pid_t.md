### 5.2.3　pid_t

从编程角度看，进程ID是由数据类型pid_t来表示的，pid_t在头文件<sys/types.h>中定义。pid_t对应的具体的C语言类型是与机器的体系结构相关的，并且在任何C语言标准中都没有定义它。但是，在Linux中，pid_t通常定义为C语言的int类型。

