### 1.2　构建一个Docker应用程序

现在，我们要动手使用Docker来构建一个简单的“to-do”应用程序（todoapp）镜像了。在这个过程中，读者会看到一些关键的Docker功能，如Dockerfile、镜像复用、端口公开及构建自动化。这是接下来10分钟读者将学到的东西：

+ 如何使用Dockerfile来创建Docker镜像；
+ 如何为Docker镜像打标签以便引用；
+ 如何运行新建的Docker镜像。

to-do应用是协助用户跟踪待完成事项的一个应用程序。我们所构建的应用将存储并显示可被标记为已完成的信息的简短字符串，它以一个简单的网页界面呈现。图1-6展示了如此操作将得到的结果。

![10.png](../images/10.png)
<center class="my_markdown"><b class="my_markdown">图1-6　构建一个Docker应用程序</b></center>

应用程序的细节不是重点。我们将演示的是，读者可以从我们所提供的一个简短的Dockerfile放心地在自己的宿主机上使用与我们相同的方法构建、运行、停止和启动一个应用程序，而无须考虑应用程序的安装或依赖。这正是 Docker为我们提供的关键部分——可靠地重现并简便地管理和共享开发环境。这意味着用户无须再遵循并迷失在那些复杂的或含糊的安装说明中。



**注意**

这个to-do应用程序将贯穿本书，多次使用，它非常适合用于实践和演示，因此值得读者熟悉一下。



