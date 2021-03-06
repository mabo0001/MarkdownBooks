### 9.2　推动Docker镜像的部署

在尝试实现CD时，首要的问题是将构建过程的产出移动到合适的位置。如果对CD流水线中所有场景使用同一个注册中心，看起来问题好像是解决了。但这并未涵盖CD的一个关键方面。

CD背后的关键思想之一是 **构建提升** ：流水线的每个场景（用户验收测试、集成测试以及性能测试）只有在前一个场景成功时才能触发下一个场景。使用多个注册中心时，只在某个构建场景通过时才将其提交到下一个注册中心中，就可确保使用的是 **提升后** 的构建。

接下来讲述在注册中心间迁移镜像的几种方法，甚至有一个无须注册中心即可共享Docker对象的方法。

