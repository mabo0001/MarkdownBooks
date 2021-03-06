### 第3章　将Docker用作轻量级虚拟机

**本章主要内容**

+ 将虚拟机转换成Docker镜像
+ 管理容器的服务启动
+ 在工作的时候随时保存成果
+ 在机器上管理Docker镜像
+ 在Docker Hub上分享镜像
+ 以Docker在2048里获胜

自本世纪以来，虚拟机（virtual machine，VM）已经在软件开发和部署等领域广泛普及。机器到软件的抽象使互联网时代下的软件和服务的更替及控制变得更加轻松和廉价。



**提示**

一台虚拟机即是一个模拟真实计算机的应用，它通常会运行一个操作系统和一些应用。它可以被放到任何（兼容的）可用的物理资源上。最终用户的软件体验就好像在物理机上一样，而那些管理硬件的人员则可以专注于大规模的资源分配。



Docker并不是一项虚拟机技术。它不会模拟一台机器的硬件，也不会包括一个操作系统。一般情况下，一个Docker容器没有指定硬件限制的约束。如果说Docker抽象了什么的话，那便是它将服务运行的环境而不是机器本身虚拟化了。此外，Docker很难运行Windows软件（甚至为其他Unix衍生的操作系统编写的软件）。

虽说从某些方面来看，可以把Docker当成一台虚拟机使用，但事实上，对互联网时代的开发人员和测试人员而言，有没有初始化进程或者是否直接和硬件交互并没有什么重大意义。而Docker和虚拟机有一些显著的共性，例如它对周围硬件具有较好的隔离性以及顺应更加细粒度的软件交付方式。

本章将会带领读者领略一些之前使用虚拟机但如今可以用Docker实现的场景。相比于虚拟机，使用Docker不会给用户带来任何明显的功能优势，但是Docker在更替和环境跟踪方面带来的速度及便利性也许可以改写开发流水线的游戏规则。

