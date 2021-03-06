### 第18章 LCD设备驱动

在多媒体应用的推动下，彩色LCD越来越多地应用到了嵌入式系统中，掌上电脑（PDA）、手机等多采用TFT显示器件，支持彩色图形界面，能显示图片并进行视频媒体播放。帧缓冲（Framebuffer）是Linux为显示设备提供的一个接口，它允许上层应用程序在图形模式下直接对显示缓冲区进行读写操作。

本章主要讲解帧缓冲设备Linux驱动的架构及编程方法。

18.1节讲解了LCD的底层硬件操作原理，18.2节讲解了帧缓冲设备的概念及驱动中的重要数据结构和函数。

18.3节讲解了帧缓冲设备驱动的整体结构，18.4～18.8节分别讲解了帧缓冲设备的几个重要函数，18.3节和18.4～18.8节的内容是整体与部分的关系。

18.9节讲解了Linux帧缓冲设备用户空间的访问方法，并对Qt/Embedded、MiniGUI、MicroWindows、Android等GUI进行了简单的介绍。

18.10节讲解了S3C6410 LCD控制器设备驱动的实例。



