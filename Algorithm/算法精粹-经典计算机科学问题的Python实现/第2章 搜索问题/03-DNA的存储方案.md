### 2.1.1　DNA的存储方案

核苷酸可以表示为包含4种状态的简单类型 `IntEnum` ，如代码清单2-1所示。

代码清单2-1　dna_search.py

```c
from enum import IntEnum
from typing import Tuple, List
Nucleotide: IntEnum = IntEnum('Nucleotide', ('A', 'C', 'G', 'T'))

```

`Nucleotide` 的类型是 `IntEnum` ，而不仅仅是 `Enum` ，因为 `IntEnum` “免费”提供了比较运算符（<、>=等）。为了使要实现的搜索算法能完成这些操作，需要数据类型支持这些运算符。从 `typing` 包中导入 `Tuple` 和 `List` ，是为了获得类型提示提供的支持。

如代码清单2-2所示， `Codon` 可以定义为包含3个 `Nucleotide` 的元组， `Gene` 可以定义为 `Codon` 的列表。

代码清单2-2　dna_search.py（续）

```c
Codon = Tuple[Nucleotide, Nucleotide, Nucleotide]  # type alias for codons
Gene = List[Codon]  # type alias for genes

```



**注意** 　尽管稍后需要对 `Codon` 进行相互比较，但是此处并不需要为 `Codon` 定义显式地实现了“<”操作符的自定义类，这是因为只要组成元组的元素类型是可比较的，Python就内置支持元组的比较操作。



互联网上的基因数据通常都是以文件格式提供的，其中包含了代表基因序列中所有核苷酸的超长字符串。下面将为某个虚构的基因定义这样一个字符串，并将其命名为 `gene_str` ，具体代码如代码清单2-3所示。

代码清单2-3　dna_search.py（续）

```c
gene_str: str = "ACGTGGCTCTCTAACGTACGTACGTACGGGGTTTATATATACCCTAGGACTCCCTTT"
```

这里还需要一个实用函数把 `str` 转换为 `Gene` 。具体代码如代码清单2-4所示。

代码清单2-4　dna_search.py（续）

```c
def string_to_gene(s: str) -> Gene:
    gene: Gene = []
    for i in range(0, len(s), 3):
        if (i + 2) >= len(s):  # don't run off end!
           return gene
        # initialize codon out of three nucleotides
        codon: Codon = (Nucleotide[s[i]], Nucleotide[s[i + 1]], Nucleotide[s[i + 2]])
        gene.append(codon)  # add codon to gene
    return gene

```

`string_to_gene()` 遍历给定的 `str` ，把每3个字符转换为 `Codon` ，并将其追加到新建的 `Gene` 的末尾。如果该函数发现从正在读取的 `s` 的当前位置开始不够放下两个 `Nucleotide` 的位置（参见循环中的 `if` 语句），就说明已经到达不完整基因的末尾了，于是最后一个或两个核苷酸就会被跳过。

`string_to_gene()` 可用于把 `str` 类型的 `gene_str` 转换为 `Gene` 。具体代码如代码清单2-5所示。

代码清单2-5　dna_search.py（续）

```c
my_gene: Gene = string_to_gene(gene_str)
```

