### 2.4.2　打造自己的Linux发行版

你可以自己组装嵌入式项目所需的所有元件。但要知道这样做的风险，以及是否值得为此付出。如果你纯粹出于兴趣而专注于嵌入式Linux，比如参与一个兴趣小组或大学里的项目，自己做是个不错的选择。然而，如果是做项目你就需要斟酌了，将项目所需的所有工具和实用程序组装在一起，并保证它们之间能够兼容是需要花费大量时间的。

新手需要一个工具链。gcc和binutils都可以从<a class="my_markdown" href="['http://www.fsf.org']">www.fsf.org</a>及遍布世界的镜像网站获得。在一个项目中，这两个工具都是编译内核和用户空间应用程序所必需的。这些工具主要是以源码的方式发布的，所以你必须自行编译，以适合特定的交叉开发环境。在获得这些实用程序的最新 “稳定版”源码后，你通常还需要对这些源码打补丁，特别是当这些程序用于非x86/IA32架构的系统时。这些补丁程序一般都和基本的软件包存放在同一位置。你所面对的挑战就是找到那些合适的补丁程序，以满足特定问题或架构的需要。

准备好工具链以后，你还需要下载和编译很多应用程序软件包，以及它们所依赖的软件包。这是一个不小的挑战，因为很多软件包即使发展到今天也不便于交叉编译。很多软件包都是在x86环境下开发的，如果转换到其他环境下，仍然会出现编译等类似问题。

挑战并未到此结束，你也许想搭建一个全能的开发环境，包含很多工具，比如图形化调试器、内存分析工具、系统跟踪和性能分析工具等。从这里的讨论你可以看到，搭建你自己的嵌入式Linux发行版是一项相当艰巨的任务。

