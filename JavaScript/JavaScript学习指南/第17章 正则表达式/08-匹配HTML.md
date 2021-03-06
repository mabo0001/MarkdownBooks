### 17.7　匹配HTML

在之前的例子中，作者用正则表达式执行了一个很常见的任务：匹配HTML。虽然这只是一个常见任务，但也必须提醒大家，通过使用正则表达式，能用HTML做很多有用的事情，但却不能用正则表达式解析HTML。解析表示将东西全部拆分成组件。正则表达式只能解析正规的语言（顾名思义）。正规语言非常简单，在绝大多数时候，只会在更加复杂的语言上使用正则表达式。既然正则表达式可以在更加复杂的语言上物尽其用，那为什么不能用来解析HTML呢？因为一定要先搞清楚正则表达式的不足，才能知道到什么时候应该使用更强大的工具。即使正则表达式在HTML上是有用的，但是未来会出现的正则表达式所不能应付的HTML，这也是有可能的。为了完美地解决这个问题，这里需要引入一个解析器。来看一个例子：

```javascript
const html = '<br> [!CDATA[[<br>]]';
const matches = html.match(/<br>/ig);
```

在这个例子中，正则表达式会匹配两次，但其实只有一个真正的<br>标签，另一个匹配的字符串只是一个非HTML字符（CDATA）。除此之外，正则表达式在匹配具有等级结构的内容时也会受限（例如，<p>标签内部的<a>标签）。从理论上解释这些限制因素已经远远超出了本书的范围，但要记住一点：如果正在纠结于构建一个正则表达式去匹配非常复杂的东西（例如HTML），那么就该考虑一下它是否是一个合适的工具。

