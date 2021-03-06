### 20.12　复习PyAutoGUI的函数

本章介绍了许多不同函数，下面是快速的汇总参考。

`moveTo(x, y)：` 将鼠标指针移动到指定的x、y坐标。

`move(xOffset, yOffset)：` 相对于当前位置移动鼠标指针。

`dragTo(x, y)：` 按住左键移动鼠标指针。

`drag(xOffset, yOffset)：` 按住左键，相对于当前位置移动鼠标指针。

`click(x, y, button)：` 模拟单击（默认是左键）。

`rightClick()：` 模拟右键单击。

`middleClick()：` 模拟中键单击。

`doubleClick()：` 模拟左键双击。

`mouseDown(x, y, button)：` 模拟在x、y处按指定的鼠标按键。

`mouseUp(x, y, button)：` 模拟在x、y处释放指定键。

`scroll(units)：` 模拟滚动滚轮。正参数表示向上滚动，负参数表示向下滚动。

`write(message)：` 输入指定message字符串中的字符。

`write([key1, key2, key3])：` 输入指定键字符串。

`press(key)：` 按下并释放指定键。

`keyDown(key)：` 模拟按下指定键。

`keyUp(key)：` 模拟释放指定键。

`hotkey([key1, key2, key3])：` 模拟按顺序按下指定键，然后以相反的顺序释放。

`screenshot()：` 返回屏幕快照的 `Image` 对象（参见第19章关于 `Image` 对象的信息）。

`getActiveWindow()` 、 `getAllWindows()` 、 `getWindowsAt()` 和 `getWindowsWithTitle()：` 返回Window对象，可通过该对象在桌面上调整应用程序窗口的大小和位置。

`getAllTitles()` 返回桌面上每个窗口的标题栏文本的字符串列表。



**captchas和计算机道德**

“用完全自动化的公共图灵测试来区分计算机和人类”或“captchas”是指那些小测试，要求你输入扭曲图片上的字母，或单击消防栓的图片。这些测试对人类来说很容易通过（尽管很烦人），但对软件来说几乎不可能解决。看完这一章，你就会知道写一个脚本是多么容易，例如，可以注册几十亿个免费的电子邮件账户，或者用大量骚扰信息攻击用户。captchas要求完成只有人类才能通过的步骤，从而缓解这种情况。

然而，并不是所有的网站都能实现captchas，而且这些很容易被不道德的程序员滥用。编程是一项强大而激动人心的技能，你可能受到诱惑去滥用这种能力，以谋取个人利益，甚至只是为了炫耀。但是，就像一扇没锁的门并不能成为非法入侵的理由一样，你的程序的责任也应该由你这个程序员来承担。绕过系统造成伤害，侵犯隐私，或者获得不正当的利益，这些并没有什么高明之处。我希望我在写这本书的过程中所做的努力，能让你成为最有成就感的自己，而不是唯利是图的自己。



