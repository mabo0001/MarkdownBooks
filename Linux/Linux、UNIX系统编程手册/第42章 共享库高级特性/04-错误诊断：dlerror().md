### 42.1.2　错误诊断：dlerror()

如果在dlopen()调用或dlopen API的其他函数调用中得到了一个错误，那么可以使用dlerror()来获取一个指向表明错误原因的字符串的指针。



![1076.png](../images/1076.png)
如果从上一次调用dlerror()到现在没有发生错误，那么dlerror()函数返回NULL，读者在下一节中就会看到这种处理方式带来的好处了。

