### 2.3　 `search` 包

这个程序使用的框架和业务逻辑都在 `search` 包里。这个包由4个不同的代码文件组成，每个文件对应一个独立的职责。我们会逐步分析这个程序的逻辑，到时再说明各个代码文件的作用。

由于整个程序都围绕匹配器来运作，我们先简单介绍一下什么是匹配器。这个程序里的匹配器，是指包含特定信息、用于处理某类数据源的实例。在这个示例程序中有两个匹配器。框架本身实现了一个无法获取任何信息的默认匹配器，而在 `matchers` 包里实现了RSS匹配器。RSS匹配器知道如何获取、读入并查找RSS数据源。随后我们会扩展这个程序，加入能读取JSON文档或CSV文件的匹配器。我们后面会再讨论如何实现匹配器。

