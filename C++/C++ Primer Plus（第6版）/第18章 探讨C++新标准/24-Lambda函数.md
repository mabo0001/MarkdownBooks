### 18.4　Lambda函数

见到术语lambda函数（也叫lambda表达式，常简称为lambda）时，您可能怀疑C++11添加这项新功能旨在帮助编程新手。看到下面的lambda函数示例后，您可能坚定了自己的怀疑：

```css
[&count](int x){count += (x % 13 == 0);}
```

但lambda函数并不像看起来那么晦涩难懂，它们提供了一种有用的服务，对使用函数谓词的STL算法来说尤其如此。

