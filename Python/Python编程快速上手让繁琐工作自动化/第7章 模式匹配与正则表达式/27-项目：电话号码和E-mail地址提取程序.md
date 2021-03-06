### 7.15　项目：电话号码和E-mail地址提取程序

假设你有一个任务：要在一篇长的网页或文章中，找出所有的电话号码和E-mail地址。如果手动翻页，可能需要查找很长时间。如果有一个程序，可以在剪贴板的文本中查找电话号码和E-mail地址，那你就只要按Ctrl-A快捷键选择所有文本，再按Ctrl-C快捷键将它复制到剪贴板，然后运行你的程序，它就会用找到的电话号码和E-mail地址替换掉剪贴板中的文本。

当你开始接手一个新项目时，很容易想要直接开始写代码。但更多的时候，最好是后退一步，考虑更大的图景。我建议先草拟高层次的计划，弄清楚程序需要做什么。暂时不要思考真正的代码，稍后再来考虑。现在，先关注大框架。

例如，你的电话号码和E-mail地址提取程序需要完成以下任务。

1．从剪贴板取得文本。

2．找出文本中所有的电话号码和E-mail地址。

3．将它们粘贴到剪贴板。

现在你可以开始思考如何用代码来完成工作。代码需要执行以下操作。

1．使用 `pyperclip` 模块复制和粘贴字符串。

2．创建两个正则表达式，一个匹配电话号码，另一个匹配E-mail地址。

3．对两个正则表达式，找到所有的匹配，而不只是第一次匹配。

4．将匹配的字符串整理好格式放在一个字符串中，用于粘贴。

5．如果文本中没有找到匹配，则显示某种消息。

这个列表就像项目的路线图。在编写代码时，可以独立地关注其中的每一步。每一步都很好管理。它的表达方式让你知道在Python中如何去做。

