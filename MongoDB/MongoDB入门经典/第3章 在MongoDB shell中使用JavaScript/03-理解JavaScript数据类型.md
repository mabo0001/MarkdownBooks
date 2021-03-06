### 3.2　理解JavaScript数据类型

JavaScript根据数据类型来决定如何处理赋给变量的数据。变量的类型决定了您可对变量执行哪些操作，如循环和执行。下面是您在本书中最常用的变量类型。

+ **字符串** ：这种变量以字符串的方式存储字符数据。字符数据用单引号或双引号标识，引号内的所有数据都将赋给字符串变量，例如：

```go
var myString = 'Some Text';
var anotherString = 'Some More Text';
```

+ **数字** ：以数值方式存储的数据。数字在计数、计算和比较时很有用。下面是一些示例：

```go
var myInteger = 1;
var cost = 1.33;
```

+ **布尔型** ：这种变量存储一位，其值要么为true要么为false。布尔值常用作标志，例如您可能在代码开头将一个变量设置为false，并在代码末尾检查该变量，以确定代码执行时是否经过了特定的位置。下面的示例定义了一个值为true的变量和一个值为false的变量：

```go
var yes = true;
var no = false;
```

+ **数组** ：使用索引的数组是一系列不同的数据项，它们存储在一个变量名下。要访问数组中的数据项，可使用array[index]，其中index是从零开始的索引。在下面的示例中，创建了一个简单的数组，再访问第一个元素（其索引为0）。

```go
var arr = ["one", "two", "three"];
var first = arr[0];
```

+ **对象字面量** ：在JavaScript中，可创建和使用对象字面量。使用对象字面量时，可使用语法object.property来访问对象的值和函数。下面的示例演示了如何创建和访问对象字面量的属性：

```go
var obj = {"name":"Brad", "occupation":"Hacker", "age", "Unknown"};
var name = obj.name;
```

+ **null** ：有时候，您没有在变量中存储值，这可能是因为它还没有创建或您不想再使用它。在这种情况下，可将变量设置为null。使用null比将值0或空字符串""赋给变量更佳，因为这些值对变量来说可能是有效的值。将null赋给变量表示它没有值，可在代码中将其与null进行比较。

```go
var newVar = null;
```

提示：

> JavaScript是一种无类型语言，您无需给变量指定数据类型——解释器会自动确定变量的正确类型。另外，可将一种类型的值赋给另一种类型的变量，例如，下面的代码定义了一个字符串变量，然后将一个整型值赋给它：

```go
var id = "testID";
id = 1;
```

