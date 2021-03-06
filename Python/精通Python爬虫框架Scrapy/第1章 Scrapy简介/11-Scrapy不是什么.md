### 1.6　Scrapy不是什么

最后，很容易误解Scrapy可以为你做什么，主要是因为数据抓取这个术语与其相关术语有些模糊，很多术语是交替使用的。我将尝试使这些方面更加清楚，以防止混淆，为你节省一些时间。

Scrapy不是Apache Nutch，也就是说，它不是一个通用的网络爬虫。如果Scrapy访问一个一无所知的网站，它将无法做出任何有意义的事情。Scrapy是用于提取结构化信息的，需要人工介入，设置合适的XPath或CSS表达式。而Apache Nutch则是获取通用页面并从中提取信息，比如关键字。它可能更适合于一些应用，但对另一些应用则又更不适合。

Scrapy不是Apache Solr、Elasticsearch或Lucene，换句话说，就是它与搜索引擎无关。Scrapy并不打算为你提供包含“Einstein”或其他单词的文档的参考。你可以使用Scrapy抽取数据，然后将其插入到Solr或Elasticsearch当中，我们会在第9章的开始部分讲解这一做法，不过这仅仅是使用Scrapy的一个方法，而不是嵌入在Scrapy内的功能。

最后，Scrapy不是类似MySQL、MongoDB或Redis的数据库。它既不存储数据，也不索引数据。它只用于抽取数据。即便如此，你可能会将Scrapy抽取得到的数据插入到数据库当中，而且它对很多数据库也都有所支持，能够让你的生活更加轻松。然而Scrapy终究不是一个数据库，其输出也可以很容易地更改为只是磁盘中的文件，甚至什么都不输出——虽然我不确定这有什么用。

