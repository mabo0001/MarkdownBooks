#### B.9.6　指向 `void` 的指针

C++可以把任意类型的指针赋给指向 `void` 的指针，这点与C相同。但是不同的是，只有使用显式强制类型转换才能把指向 `void` 的指针赋给其他类型的指针。下面的代码说明了这一点：

```c
int ar[5] = {4, 5, 6,7, 8};
int * pi;
void * pv;
pv = ar;            /* C和C++都可以 */
pi = pv;            /* C可以，C++不可以 */
pi = (int * ) pv;   /* C和C++都可以 */
```

C++与C的另一个区别是，C++可以把派生类对象的地址赋给基类指针，但是在C中没有这里涉及的特性。

