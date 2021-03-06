### 9.2　有效用户ID和有效组ID

在大多数UNIX实现（Linux实现略有差异，具体参见9.5节的说明）中，当进程尝试执行各种操作（即系统调用）时，将结合有效用户ID、有效组ID，连同辅助组ID一起来确定授予进程的权限。例如，当进程访问诸如文件、System V进程间通信（IPC）对象之类的系统资源时，此类ID会决定系统授予进程的权限，而这些资源的属主则另由与之相关的用户ID和组ID来决定。如20.5节所述，内核还会使用有效用户ID来决定一个进程是否能向另一个进程发送信号。

有效用户ID为0（root的用户ID）的进程拥有超级用户的所有权限。这样的进程又称为特权级进程（privileged process）。而某些系统调用只能由特权级进程执行。

> 第39章描述了Linux实现的能力（capability）方案，即把授予给超级用户的特权划分为若干不同单元，且能独立启用和禁用这些单元。

通常，有效用户ID及组ID与其相应的实际ID相等，但有两种方法能够致使二者不同。其一是使用9.7节中所讨论的系统调用，其二是执行set-user-ID和set-group-ID程序。

