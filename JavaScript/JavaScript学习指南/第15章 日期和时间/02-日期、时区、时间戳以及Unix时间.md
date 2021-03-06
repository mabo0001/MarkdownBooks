### 15.1　日期、时区、时间戳以及Unix时间

事实是，现代的公历非常繁琐复杂，比如，时间是从1计数，奇怪的划分时间方式，以及闰年的出现。时区的计算更是增加了这种复杂度。然而必须面对它，因为它很通用。

我们从简单的内容开始：秒。不像公历中复杂的时间划分，秒很简单。日期和时间当用秒表示的时候，只是一个数字，在数轴上均匀排列。用秒表示日期和时间，是为了更好地计算。然而，它并不是沟通友好的：“Hey，Byron，想在第1 437 595 200秒一起吃午餐吗？”（1 437 595 200表示2015.7.22 13:00周三，太平洋标准时间）。如果日期使用秒来表示，那么0表示什么日期呢？事实上，它并不代表耶稣诞生，它只是一个普通的时间：1970年1月1日 00:00:00 UTC。

大家可能已经知道，世界被划分为不同的时区（TZs），所以不论在哪里，7:00 AM都是早上，7:00 PM都是晚上。时区可以迅速地变复杂，尤其是把夏令时也考虑进来以后。作者不打算在本书中解释关于公历和时区的所有细节，维基百科上已经解释的很好了。然而，掌握一些基础知识还是很重要的，这有助于更好地理解JavaScript的Date对象（以及Moment.js带来的好处）。

所有时区都定义为以协调世界时（Coordinated Universal Time，缩写为UTC。通过查阅维基百科可以了解命名背后复杂却有趣的原因）为基准的时间偏移量。有时候，UTC（并不完全正确）也叫格林威治标准时间（GMT）。例如，处在太平洋时区的俄勒冈州，太平洋时间比UTC晚7～8个小时。7～8？到底是哪个呢？其实这取决于季节。比如，夏天处在夏令时，时差是7个小时。而其他时候则是标准时间，时差为8个小时。关于时区，重点不是记住它们，而是理解如何表示不同时区的时间偏移量。打开一个JavaScript console，输入new Date()，就会看到如下内容：

```javascript
Sat Jul 18 2015 11:07:06 GMT-0700 (太平洋时间)
```

注意，在这个冗长的格式中，时区由两种信息组成：相比于UTC的偏移量，和时区的名字（太平洋时间）。

在JavaScript中，所有 `Date` 实例都被存储成一个数字：距离Unix新纪元（1970年1月1日00:00:00）的毫秒数（不是秒）。不论何时请求一个Date实例（就像刚才看到的），JavaScript会将那个数字转换成人们可以读懂的公历日期。如果想看日期的数字表示，调用 `valueOf()` 方法即可：

```javascript
const d = new Date();
console.log(d);               // 使用TZ格式化后的公历日期
console.log(d.valueOf());     // 距离Unix新纪元的毫秒数
```

