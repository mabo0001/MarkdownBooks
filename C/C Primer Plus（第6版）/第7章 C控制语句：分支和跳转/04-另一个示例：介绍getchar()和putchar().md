#### 7.2.1　另一个示例：介绍 `getchar()` 和 `putchar()` 

到目前为止，学过的大多数程序示例都要求输入数值。接下来，我们看看输入字符的示例。相信读者已经熟悉了如何用 `scanf()` 和 `printf()` 根据 `%c` 转换说明读写字符，我们马上要讲解的示例中要用到一对字符输入 `/` 输出函数： `getchar()` 和 `putchar()` 。

`getchar()` 函数不带任何参数，它从输入队列中返回下一个字符。例如，下面的语句读取下一个字符输入，并把该字符的值赋给变量 `ch` ：

```c
ch = getchar();
```

该语句与下面的语句效果相同：

```c
scanf("%c", &ch);
```

`putchar()` 函数打印它的参数。例如，下面的语句把之前赋给 `ch` 的值作为字符打印出来：

```c
putchar(ch);
```

该语句与下面的语句效果相同：

```c
printf("%c", ch);
```

由于这些函数只处理字符，所以它们比更通用的 `scanf()` 和 `printf()` 函数更快、更简洁。而且，注意 `getchar()` 和 `putchar()` 不需要转换说明，因为它们只处理字符。这两个函数通常定义在 `stdio.h` 头文件中（而且，它们通常是预处理宏，而不是真正的函数，第16章会讨论类似函数的宏）。

接下来，我们编写一个程序来说明这两个函数是如何工作的。该程序把一行输入重新打印出来，但是每个非空格都被替换成原字符在ASCII序列中的下一个字符，空格不变。这一过程可描述为“如果字符是空白，原样打印；否则，打印原字符在ASCII序列中的下一个字符”。

C代码看上去和上面的描述很相似，请看程序清单7.2。

程序清单7.2　 `cypher1.c` 程序

```c
// cypher1.c -- 更改输入，空格不变
#include <stdio.h>
#define SPACE ' '                  // SPACE表示单引号-空格-单引号
int main(void)
{
     char ch;
     ch = getchar();              // 读取一个字符
     while (ch != '\n')           // 当一行未结束时
     {
          if (ch == SPACE)        // 留下空格
               putchar(ch);       // 该字符不变
          else
               putchar(ch + 1);   // 改变其他字符
          ch = getchar();         // 获取下一个字符
     }
     putchar(ch);                 // 打印换行符
     return 0;
}
```

（如果编译器警告因转换可能导致数据丢失，不用担心。第8章在讲到 `EOF` 时再解释。）

下面是该程序的输入示例：

```c
CALL ME HAL.
DBMM NF IBM/

```

把程序清单7.1中的循环和该例中的循环作比较。前者使用 `scanf()` 返回的状态值判断是否结束循环，而后者使用输入项的值来判断是否结束循环。这使得两程序所用的循环结构略有不同：程序清单7.1中在循环前面有一条“读取语句”，程序清单7.2中在每次迭代的末尾有一条“读取语句”。不过，C的语法比较灵活，读者也可以模仿程序清单7.1，把读取和测试合并成一个表达式。也就是说，可以把这种形式的循环：

```c
ch = getchar();         /* 读取一个字符 */
while (ch != '\n')      /* 当一行未结束时 */
{
     ...                /* 处理字符 */
     ch = getchar();    /* 获取下一个字符 */
}
```

替换成下面形式的循环：

```c
while ((ch = getchar()) != '\n')
{
     ...                /* 处理字符 */
}
```

关键的一行代码是：

```c
while ((ch = getchar()) != '\n')
```

这体现了C特有的编程风格——把两个行为合并成一个表达式。C对代码的格式要求宽松，这样写让其中的每个行为更加清晰：

```c
while (
         (ch = getchar())             // 给ch赋一个值
                          != '\n')    // 把ch和\n作比较
```

以上执行的行为是赋值给 `ch` 和把 `ch` 的值与换行符作比较。表达式 `ch = getchar()` 两侧的圆括号使之成为 `!=` 运算符的左侧运算对象。要对该表达式求值，必须先调用 `getchar()` 函数，然后把该函数的返回值赋给 `ch` 。因为赋值表达式的值是赋值运算符左侧运算对象的值，所以 `ch = getchar()` 的值就是 `ch` 的新值，因此，读取 `ch` 的值后，测试条件相当于是 `ch != '\n'` （即， `ch` 不是换行符）。

这种独特的写法在C编程中很常见，应该多熟悉它。还要记住合理使用圆括号组合子表达式。上面例子中的圆括号都必不可少。假设省略 `ch = getchar()` 两侧的圆括号：

```c
while (ch = getchar() != '\n')
```

!=运算符的优先级比=高，所以先对表达式 `getchar() != '\n'` 求值。由于这是关系表达式，所以其值不是1就是0（真或假）。然后，把该值赋给 `ch` 。省略圆括号意味着赋给 `ch` 的值是 `0` 或 `1` ，而不是 `getchar()` 的返回值。这不是我们的初衷。

下面的语句：

```c
putchar(ch + 1); /* 改变其他字符 */
```

再次演示了字符实际上是作为整数存储的。为方便计算，表达式 `ch + 1` 中的 `ch` 被转换成 `int` 类型，然后 `int` 类型的计算结果被传递给接受一个 `int` 类型参数的 `putchar()` ，该函数只根据最后一个字节确定显示哪个字符。

