### 现代前端Web应用的路由

过去，Web应用的基本架构使用了一种不同于现代路由的方法。旧方法涉及服务器（想一想用Python、Ruby或PHP创建的东西）生成HTML标记并将标记下发到浏览器。用户可能会在表单里填写一些数据，然后再将数据提交给服务器并等待响应。这在使Web更强大方面是革命性的进步，因为用户能够修改数据而不只是查看数据。

自那时起，Web服务在设计和构造方面经历了很多发展。如今，JavaScript框架和浏览器技术已经足够先进，以至于Web应用可以采用更独特的前后端分离机制。客户端应用程序（完全在浏览器中）被服务器下发，然后客户端应用有效地“接管”工作。而后服务器负责发送原始数据，通常是JSON格式。图7-1说明并比较了这两个通用架构是如何工作的。

![50.png](./images/50.png)
<center class="my_markdown"><b class="my_markdown">图7-1　新旧Web应用架构的简单比较。在旧架构中，动态内容由服务器生成。服务器通常会从数据库中获取数据，然后使用这些数据填充要发送给客户端的HTML视图。现在，客户端上拥有更多JavaScript管理的应用程序逻辑（这里是React）。服务器最初会下发HTML、JavaScript和CSS资源，但之后客户端React应用程序将会接管。从这里开始，除非用户手动刷新页面，否则服务器将只需下发原始JSON数据</b></center>

至此，我们一直使用现代架构构建这个用于教学的应用Letters Social。Node.js服务器发送应用程序需要的HTML、JavaScript和CSS。一旦加载完成，React就会接管。接下来的数据请求被发送到示例API服务器。但我们还缺少该架构的一个关键部分：客户端路由。



**练习7-1　路由的思考**

在深入使用React构建路由之前，花些时间思考一下路由。你在过去的项目中还遇到过哪些路由的例子？路由还有什么其他用途？



