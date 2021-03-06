### 第6章　使用MongoDB shell在MongoDB集合中查找文档

**本章介绍如下内容：**

+ 理解Cursor对象的用途；
+ 使用Cursor对象访问集合中的文档；
+ 查找单个文档；
+ 查找多个文档；
+ 使用查询运算符根据字段值查找文档；
+ 根据子文档字段查找文档。

查找文档无疑是最常见的MongoDB数据库操作。本章介绍如何访问MongoDB服务器中的文档。Collection对象提供了在服务器中查找文档的方法，您将使用这些方法来访问文档。

在这些方法中，有些返回一个Cursor对象，表示服务器中的一组文档。您将学习如何使用Cursor对象来访问文档。

您还将学习如何使用查询运算符来限制数据库查询结果。查询运算符让您能够根据字段值、字段是否存在、长度等来限制查询结果。

