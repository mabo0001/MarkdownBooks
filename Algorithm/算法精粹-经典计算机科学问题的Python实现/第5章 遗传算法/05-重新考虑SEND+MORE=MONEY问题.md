### 5.4　重新考虑SEND+MORE=MONEY问题

在第3章中，我们用约束满足框架解决了传统的数字密码问题SEND+MORE=MONEY。要获得有关该问题的全部内容，请回顾第3章中的介绍。SEND+MORE=MONEY问题也可以由遗传算法在合理的时间内得以求解。

要表达清楚遗传算法求解方案要解决的问题，最大的困难之一就是确定问题的表示形式。对数字密码问题而言，有一种便利的表示形式就是把列表索引用作数字<sup class="my_markdown">[2]</sup>。因此，为了表示要用到的10个数字（0, 1, 2, 3, 4, 5, 6, 7, 8, 9），需要采用包含10个元素的列表。其次，问题中待查找的字符可以在不同位置上相互调换。例如，如果怀疑某个问题的解中包括代表数字4的字符“E”，就让 `list[4] = "E"` 。SEND + MORE = MONEY有8个不同的字母（S, E, N, D, M, O, R, Y），于是数组中会留下2个空位。我们可以在空位中填入空格，表示此处没有字母。

代表SEND+MORE=MONEY问题的染色体用 `SendMoreMoney2` 表示。注意， `fitness()` 方法与第3章中 `SendMoreMoneyConstraint` 的 `satisf()` 方法惊人地相似。具体代码如代码清单5-11所示。

代码清单5-11　send_more_money2.py

```c
from __future__ import annotations
from typing import Tuple, List
from chromosome import Chromosome
from genetic_algorithm import GeneticAlgorithm
from random import shuffle, sample
from copy import deepcopy
class SendMoreMoney2(Chromosome):
    def __init__(self, letters: List[str]) -> None:
        self.letters: List[str] = letters
    def fitness(self) -> float:
        s: int = self.letters.index("S")
        e: int = self.letters.index("E")
        n: int = self.letters.index("N")
        d: int = self.letters.index("D")
        m: int = self.letters.index("M")
        o: int = self.letters.index("O")
        r: int = self.letters.index("R")
        y: int = self.letters.index("Y")
        send: int = s * 1000 + e * 100 + n * 10 + d
        more: int = m * 1000 + o * 100 + r * 10 + e
        money: int = m * 10000 + o * 1000 + n * 100 + e * 10 + y
        difference: int = abs(money - (send + more))
        return 1 / (difference + 1)
    @classmethod
    def random_instance(cls) ->SendMoreMoney2:
        letters = ["S", "E", "N", "D", "M", "O", "R", "Y", " ", " "]
        shuffle(letters)
        return SendMoreMoney2(letters)
    def crossover(self, other: SendMoreMoney2) -> Tuple[SendMoreMoney2, SendMoreMoney2]:
        child1: SendMoreMoney2 = deepcopy(self)
        child2: SendMoreMoney2 = deepcopy(other)
        idx1, idx2 = sample(range(len(self.letters)), k=2)
        l1, l2 = child1.letters[idx1], child2.letters[idx2]
        child1.letters[child1.letters.index(l2)], child1.letters[idx2] = child1.
         letters[idx2], l2
        child2.letters[child2.letters.index(l1)], child2.letters[idx1] = child2.
         letters[idx1], l1
        return child1, child2
    def mutate(self) -> None: # swap two letters' locations
        idx1, idx2 = sample(range(len(self.letters)), k=2)
        self.letters[idx1], self.letters[idx2] = self.letters[idx2], self.letters[idx1]
    def __str__(self) -> str:
        s: int = self.letters.index("S")
        e: int = self.letters.index("E")
        n: int = self.letters.index("N")
        d: int = self.letters.index("D")
        m: int = self.letters.index("M")
        o: int = self.letters.index("O")
        r: int = self.letters.index("R")
        y: int = self.letters.index("Y")
        send: int = s * 1000 + e * 100 + n * 10 + d
        more: int = m * 1000 + o * 100 + r * 10 + e
        money: int = m * 10000 + o * 1000 + n * 100 + e * 10 + y
        difference: int = abs(money - (send + more))
        return f"{send} + {more} = {money} Difference: {difference}"

```

不过，第3章中的 `satisfied()` 和这里的 `fitness()` 之间有一处重要的不同。这里返回的是 `1 / (difference + 1)` 。 `difference` 是MONEY和SEND + MORE之差的绝对值，表示染色体离问题的解的距离有多远。如果要让 `fitness()` 的值最小化，那么返回 `difference` 就可以了。但是，因为 `GeneticAlgorithm` 要追求 `fitness()` 的值最大化，所以需要将该值反转一下（值越小看起来越大），这就是要用1除以 `difference` 的原因。先给 `difference` 加上1，这样，当 `difference` 为0时就不会导致 `fitness()` 的值也为0（而是1）。表5-1演示了这一过程。

<center class="my_markdown"><b class="my_markdown">表5-1　公式1 / (difference + 1)如何生成适应度的最大值</b></center>

| `difference` | `difference + 1` | `fitness（1/(difference + 1)）` |
| :-----  | :-----  | :-----  | :-----  | :-----  |
| `0` | `1` | `1` |
| `1` | `2` | `0.5` |
| `2` | `3` | `0.25` |
| `3` | `4` | `0.125` |

记住，差越小越好，适应度越高越好。因为上述公式会导致这两个因子呈线性关系，所以效果不错。将1除以适应度是将求最小值问题转换为求最大值问题的简单方法，但它确实引入了一些偏差，因此并非万无一失<sup class="my_markdown">[3]</sup>。

`random_instance()` 用到了 `random` 模块中的 `shuffle()` 函数。 `crossover()` 在两个染色体的 `letters` 列表中选取两个随机索引，并交换两处的字母，这样最终在第1条染色体中有一个字母来自第2条染色体的同一位置，反之第2条染色体也是如此。这一交换过程是在子对象中执行的，这样在两个子对象中的字母的放置就完成了双亲的结合。 `mutate()` 将会交换 `letters` 列表中两个随机位置的元素。

将 `SendMoreMoney2` 放入 `GeneticAlgorithm` 与放入 `SimpleEquation` 一样容易。但要先警告一声：该问题相当棘手，如果参数调得不好，执行过程就会耗费很长时间。即使参数没问题，也存在一定的随机性！求解过程可能需要几秒或几分钟。具体代码如代码清单5-12所示。遗传算法的特性就是如此。

代码清单5-12　send_more_money2.py（续）

```c
if __name__ == "__main__":
   initial_population: List[SendMoreMoney2] = [SendMoreMoney2.random_instance() for _ in 
    range(1000)]
   ga: GeneticAlgorithm[SendMoreMoney2] = GeneticAlgorithm(initial_population=initial_
    population, threshold=1.0, max_generations = 1000, mutation_chance = 0.2, crossover_
    chance = 0.7, selection_type=GeneticAlgorithm.SelectionType.ROULETTE)
   result: SendMoreMoney2 = ga.run()
   print(result)iu

```

下面是运行了3代得到的输出结果，每代使用了1000个个体（如上所创建的）。不妨试试利用 `GeneticAlgorithm` 的可配置参数，以更少的个体获得类似的结果。看看用轮盘式选择法是否比用锦标赛选择法效果更好。

```c
Generation 0 Best 0.0040650406504065045 Avg 8.854014252391551e-05
Generation 1 Best 0.16666666666666666 Avg 0.001277329479413134
Generation 2 Best 0.5 Avg 0.014920889170684687
8324 + 913 = 9237 Difference: 0
```

以上结果表明SEND = 8324，MORE = 913，MONEY = 9237。这怎么可能？看起来解里少了几个字母。事实上，如果M = 0，有几种解是不可能由第3章的算法求得的。此处MORE实际上是0913，而MONEY是09237，只是0被忽略了。

