### 8.5　数组魔法：reduce

在所有数组方法中，作者最喜欢的是 `reduce` 。 `map` 方法可以转化数组中每一个元素，而 `reduce` 则可以转化整个数组。之所以叫它 `reduce` ，是因为它经常被用于将一个数组归纳成一个单独的值。比如，对数组所有元素求和或者计算它们的平均值就是几种常见的场景。然而，提供单值归纳功能可以是对象或者是其他数组——事实上， `reduce` 复制了一部分 `map` 和 `filter` （或者说，任何一个我们讲过的数组方法）的功能。

`Reduce` 像 `map` 和 `filter` 一样，允许提供一个可以控制输出的函数。在以往处理的回调函数中，第一个传入回调函数的参数一般是当前数组元素。而在 `reduce` 中，第一个参数是一个累加值，表示数组将被归纳成的值。剩下的参数就跟大家想的一样了：当前数组元素、当前元素的下标和数组的。

除了有回调函数外， `reduce` 还可以接收一个累加值的初始值（可选的）。下面来看一个简单的例子：给数组中的数字求和：

```javascript
const arr = [5, 7, 2, 4];
const sum = arr.reduce((a, x) => a += x, 0);
```

传入 `reduce` 中的函数有两个参数：累加值（ `a` ）和当前数组的元素（ `x` ）。在本例中，让累加值从 `0` 开始。由于这是第一次使用 `reduce` ，所以首先来了解一下JavaScript的操作步骤，有助于理解它的工作原理。

（1）函数（匿名）被数组的第一个元素（5）调用。a表示初始值0，x表示第一个元素的值：5。该函数返回a和x的和（还是5），这将作为下一步中a的值。

（2）函数被数组的第二个元素（7）调用。a的初始值为5（从上一步传过来的），x的值是7。函数会返回a和x的和（12），这将作为下一步中a的值。

（3）以此类推，当函数被数组的第三个元素（2）调用时。a的初始值是12，x的值为2。函数会返回a和x的和（14）。

（4）函数被数组的第四个元素，也是最后一个元素（4）调用。a的值为14，x为4。该函数会返回a和x的和（18），这也是reduce函数将会返回的值（也是接下来赋给sum的值）。

聪明的读者可能已经发现，这是一个很简单的例子，甚至不需要给a赋值。重要的是，函数返回什么（还记得吗？箭头标识符并不需要明确声明return语句），所以可以直接返回a + x。不过，在一些更复杂的例子中，可能希望对累加结果做更多操作，所以，好的习惯是尽量在函数内部修改累加结果。

在继续学习 `reduce` 那些更有趣的用法之前，先来看一种特殊情况：累加结果的初始值是 `undefined` 。在这种情况下， `reduce` 会把数组的第一个元素当做初始值，然后从数组的第二个元素开始调用函数。下面重新看一下这个例子，这次省略初始值：

```javascript
const arr = [5, 7, 2, 4];
const sum = arr.reduce((a, x) => a += x);
```

（1）函数（匿名）被数组的第二个元素（7）调用。a的初始值是5（数组第一个元素的值），x的值是7。调用后函数返回a和x的和（12），这会成为下一步的值。

（2）函数被数组的第三个元素（2）调用。a的初始者是12，x是2。函数返回a和x的和（14）。

（3）函数被数组的第四个元素（4）调用。a的值为14，x为4。函数依旧返回a和x的和（18），它就是reduce函数的返回值（同时赋值给sum）。

可以看到，这里虽少了一步函数调用，但结果是一样的。在本例（或者任何第一个元素可以作为累加结果初始值的例子）中，可以省略初始值来简化代码。

在reduce中使用原子值（数字或者字符串）是一个很常见的用法，不过如果用对象作为累加结果，其功能将会非常强大（这个用法经常被人们忽视）。比如：如果你想将一个string类型的数组按照字母顺序（以A开头的单词，以B开头的单词，等等）进行分组，然后每个组作为一个数组元素，这种情况下就可以使用对象：

```javascript
const words = ["Beachball", "Rodeo", "Angel",
    "Aardvark", "Xylophone", "November", "Chocolate",
    "Papaya", "Uniform", "Joker", "Clover", "Bali"];
const alphabetical = words.reduce((a, x) => {
    if(!a[x[0]]) a[x[0]] = [];
    a[x[0]].push(x);
    return a; }, {});
```

这个例子有点复杂，但本质上它与之前的例子是一样的。对于数组中的每个元素，函数都会检查累加结果，来判断结果中是否包含元素的第一个字母。如果不包含，就创建一个空数组（比如，当遇到 `"Beachball"` 的时候，它没有 `a.B` 的属性，这时元素的值就会被放入一个新创建的空数组中）。然后它会把元素放在对应的数组（就是刚刚创建的数组）中。最终，累加结果（a）会被返回（还记得吗，返回的结果将作为数组中下个元素调用函数时的累加结果。）

另一个相关的例子是计算统计数据。比如，计算某个数据集的平均值和变化：

```javascript
const data = [3.3, 5, 7.2, 12, 4, 6, 10.3];
// 这个计算方差的方法来源于Donald Knuth于1998年出版的
// 计算机程序设计艺术, 第三版中的第二卷: 半数值算法 
const stats = data.reduce((a, x) => {
        a.N++;
        let delta = x - a.mean;
        a.mean += delta/a.N;
        a.M2 += delta*(x - a.mean);
        return a;
    }, { N: 0, mean: 0, M2: 0 });
if(stats.N > 2) {
    stats.variance = stats.M2 / (stats.N - 1);
    stats.stdev = Math.sqrt(stats.variance);
}
```

这里再一次使用了对象作为累加结果，因为需要多个变量（mean和M2，也就是说，如果需要的话，可以用下标参数减一的方式来替换N）。

来看最后一个关于reduce的例子，它体现了reduce的灵活性，这个例子用了一个之前没用过的累加结果类型—字符串：

```javascript
const words = ["Beachball", "Rodeo", "Angel",
    "Aardvark", "Xylophone", "November", "Chocolate",
    "Papaya", "Uniform", "Joker", "Clover", "Bali"];
const longWords=words.reduce((a, w)=>w.length>6 ? a+" "+w:a,"").trim();
// longWords: "Beachball Aardvark Xylophone November Chocolate Uniform"
```

这里用了字符串作为累加结果，它存放所有长度大于6个字母的字符串。作为一个读者练习留给你：试着用 `filter` 和 `join` （一个字符串方法）重新实现这段代码。（提示：可以从思考为什么需要在 `reduce` 后调用 `trim` 开始）。

至此，希望大家已经了解了 `reduce` 的强大功能。在所有的数组方法中，它是最常用且作用最大的。

