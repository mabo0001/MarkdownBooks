[toc]

### 4.2　REPL的好处：深入理解JavaScript引擎

下列是一个非常经典的REPL示例：

```python
> 3 > 2 > 1;
false
```

这个代码片段很好地解释了REPL的用处。乍一看，你可能以为这个表达式的值是 `true` ，毕竟，3比2大，2也确实比1大。不过，在JavaScript中，关系运算符的运算顺序是从左到右，而每一个表达式的结果会作为下一次计算的输入。

在REPL中执行这段代码就可以更清楚地看到发生了什么：

```python
> 3 > 2 > 1;
false
> 3 > 2;
true
> true > 1;
false
```

现在的结果看起来就容易理解多了。我们可以看到，表达式 `3>2` 计算后的结果是 `true` 。但后面却把 `true` 跟数字 `1` 做比较。计算比较过的值之后，JavaScript做了自动数据类型转换。由于 `true` 并不比 `1` 大，所以最终结果是 `false` 。

REPL能帮我们探索更多JavaScript中的小技巧。我们希望通过在REPL中测试代码，不会再让一些非预期的结果影响我们的应用程序（比如期望结果是 `true` ，但是却返回了 `false` ）。

