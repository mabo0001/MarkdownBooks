### 4.1.7　用del语句从列表中删除值

`del` 语句将删除列表中索引处的值，列表中被删除值后面的所有值，都将向前移动一个索引。例如，在交互式环境中输入以下代码：

```javascript
>>> spam = ['cat', 'bat', 'rat', 'elephant']
>>> del spam[2]
>>> spam
['cat', 'bat', 'elephant']
>>> del spam[2]
>>> spam
['cat', 'bat']
```

`del` 语句也可用于一个简单变量，删除它，起“取消赋值”语句的作用。如果在删除之后试图使用该变量，就会遇到 `NameError` 错误，因为该变量已不存在。在实践中，你几乎永远不需要删除简单变量。 `del` 语句几乎总是用于删除列表中的值。

