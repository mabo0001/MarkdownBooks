### 3.4　关键字参数和print()函数

大多数参数是由它们在函数调用中的位置来识别的。例如， `random.randint(1, 10)` 与 `random.randint(10,1)` 不同。函数调用 `random.randint(1,10)` 将返回1到10之间的一个随机整数，因为第一个参数是范围的下界，第二个参数是范围的上界（而 `random.randint(10,1)` 会导致错误）。

但是，“关键字参数”是在函数调用时由它们前面的关键字来识别的。关键字参数通常用于“可选变元”。例如， `print()` 函数有可选的变元 `end` 和 `sep` ，分别指定在参数末尾输出什么，以及在参数之间输出什么来隔开它们。

如果运行以下程序：

```javascript
print('Hello')
print('World')
```

输出结果将会是：

```javascript
Hello
World
```

这两个字符串出现在独立的两行中，因为 `print()` 函数自动在传入的字符串末尾添加了换行符。可以设置 `end` 关键字参数，将它变成另一个字符串。例如，如果程序像这样：

```javascript
print('Hello', end='')
print('World')
```

输出结果就会像这样：

```javascript
HelloWorld
```

输出被显示在一行中，因为在 `'Hello'` 后面不再输出换行，而是输出了一个空字符串。如果需要禁用加到每一个 `print()` 函数调用末尾的换行符，这就很有用。

类似地，如果向 `print()` 函数传入多个字符串值，该函数就会自动用一个空格分隔它们。在交互式环境中输入以下代码：

```javascript
>>> print('cats', 'dogs', 'mice')
cats dogs mice
```

你可以传入 `sep` 关键字参数，替换掉默认的分隔字符串。在交互式环境中输入以下代码：

```javascript
>>> print('cats', 'dogs', 'mice', sep=',')
cats,dogs,mice
```

也可以在你编写的函数中添加关键字参数，但必须先在接下来的两章中学习列表和字典数据类型。现在只要知道，某些函数有可选的关键字参数，在函数调用时可以指定。

