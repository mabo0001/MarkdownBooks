### 第1章 NoSQL和MongoDB简介

**本章介绍如下内容：**

+ MongoDB如何组织数据；
+ MongoDB支持哪些数据类型；
+ 什么情况下该范式化数据，什么情况下该反范式化；
+ 如何规划数据模型；
+ 固定集合（capped collection）是如何工作的；
+ 什么情况下该使用索引、分片和复制；
+ 如何确定数据的生命周期。

在大多数大型应用程序和服务中，核心都是高性能的数据存储解决方案。后端数据存储负责存储用户账户信息、产品数据、记账信息和博客等重要数据。优秀的应用程序要求能够准确、快速、可靠地存储和检索数据，因此选择的数据存储机制的性能必须能够满足应用程序的需求。

有多种数据存储解决方案可用于存储和检索应用程序所需的数据，其中最常见的有三种：文件系统直接存储、关系型数据库和NoSQL数据库。本书介绍MongoDB，它是使用最广泛、功能最强大的NoSQL数据存储方式。

接下来的几节将介绍NoSQL和MongoDB，并讨论决定如何组织数据和配置数据库前需要考虑的设计因素。为此，将首先提出问题，再介绍能够满足这些需求的MongoDB内置机制。

