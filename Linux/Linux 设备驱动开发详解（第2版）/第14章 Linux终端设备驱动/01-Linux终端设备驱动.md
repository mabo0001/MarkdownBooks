### 第14章 Linux终端设备驱动

#### 本章导读

在Linux系统中，终端设备非常重要，没有终端设备，系统将无法向用户反馈信息，Linux中包含控制台、串口和伪终端3类终端设备。

14.1节讲解了终端设备的概念及分类，14.2节讲解了Linux终端设备驱动的框架结构，重点描述tty_driver结构体及其成员。

14.3～14.5节在14.2节的基础上，分别讲解了Linux终端设备驱动模块加载/卸载函数和open()、close()函数，数据读写流程及tty设备线路设置的编程方法。

在Linux中，串口驱动完全遵循tty驱动的框架结构，但是进行了底层操作的再次封装，14.6节描述了Linux针对串口tty驱动的这一封装，14.7节则具体给出了串口tty驱动的实现方法。

14.8节基于14.6和14.7节的讲解给出了串口tty驱动的设计实例，即S3C6410集成UART的驱动。



