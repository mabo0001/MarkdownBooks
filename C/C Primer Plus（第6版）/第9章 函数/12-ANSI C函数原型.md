### 9.2　ANSI C函数原型

在ANSI C标准之前，声明函数的方案有缺陷，因为只需要声明函数的类型，不用声明任何参数。下面我们看一下使用旧式的函数声明会导致什么问题。

下面是ANSI之前的函数声明，告知编译器 `imin()` 返回 `int` 类型的值：

```c
int imin();
```

然而，以上函数声明并未给出 `imin()` 函数的参数个数和类型。因此，如果调用 `imin()` 时使用的参数个数不对或类型不匹配，编译器根本不会察觉出来。

