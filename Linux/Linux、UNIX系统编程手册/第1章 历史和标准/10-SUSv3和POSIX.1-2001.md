### 1.3.4　SUSv3和POSIX.1-2001

始于1999年，出于修订并加强POSIX标准和SUS规范的目的，IEEE、Open集团以及ISO/ IEC联合技术委员会共同成立了奥斯丁公共标准修订工作组（CSRG，http://www.opengroup.org/ austin/）。（该工作组的首次会议于1998年9月在德州奥斯丁召开，这也是奥斯丁工作组名称的由来。）2001年12月，该工作组正式批准了POSIX 1003.1-2001，有时简称为POSIX.1-2001（随后，又获批为ISO标准：ISO/IEC 9945:2002）。

POSIX 1003.1-2001取代了SUSv2、POSIX.1、POSIX.2以及大批的早期POSIX标准。有时，人们也将该标准称为Single Unix Specification版本3，本书在后续内容中将称其为SUSv3。

SUSv3基本规范约有3700页，分为以下4部分。

+ 基本定义（XBD），包含了定义、术语、概念以及对头文件内容的规范。总计提供了84个头文件的规范。
+ 系统接口（XSH），首先介绍了各种有用的背景信息。主要内容包含对各种函数（在特定的UNIX实现中，这些函数要么是作为系统调用，要么是作为库函数来实现的）的定义。总计包括了1123个系统接口。
+ Shell和实用工具（XCU），明确定义了shell和各种UNIX命令的行为。总共定义了160个实用工具的行为。
+ 基本原理（XRAT），包括了与前三部分有关的描述性文字和原理说明。

此外，SUSv3还包含了X/Open CURSES第4号版本2（XCURSES）规范，该规范针对curses屏幕处理API定义了372个函数和3个头文件。

在SUSv3中共计定义了1742个接口。与之形成鲜明对照的是，POSIX.1-1990（连同FIPS 151-2）定义了199个接口，POSIX.2-1992定义了130个实用工具。

SUSv3规范可在线获得，网址是http://www.unix.org/version3/online.html。通过SUSv3认证的UNIX实现可被称为UNIX 03。

自SUSv3获批以来，人们针对规范文本中所发现的问题进行了多次小规模的修复和改进。因此而诞生的1号技术勘误表并入了2003年发布的SUSv3修订版，而2号技术勘误表的改进成果则并入了SUSv3 2004修订版。

#### 符合POSIX、XSI规范和XSI扩展

回顾历史，SUS（和XPG）标准顺应了相应POSIX标准，并被组织为POSIX的功能超集。除了对许多额外接口作出规范外，SUS标准还将诸多被POSIX视为可选的接口和行为规范作为必备项。

对于身兼IEEE标准和OPEN集团技术标准的POSIX 1003.1-2001来说（如前所述，POSIX 1003.1-2001是由早期的POSIX和SUS标准合并而成），上述区别的存在方式更显微妙。该文档定义了对规范的两级符合度。

+ POSIX规范符合度，就符合该规范的UNIX实现所必须提供的接口定义了基线。规范允许符合度达标的UNIX实现提供其他可选接口。
+ XSI（X/Open系统接口[X/Open System Interface]）规范符合度，对UNIX实现来说，要想完全符合XSI规范，除了必须满足POSIX规范的所有规定之外，还要提供若干POSIX规范中的可选接口和行为。只有这一规范符合度达标，才能从OPEN GROUP获得UNIX03称号。

人们将XSI规范符合度达标所需的额外接口和行为统称为XSI扩展。这些扩展支持以下特性：线程、mmap()和munmap()、dlopen API、资源限制、伪终端、System V IPC、syslog API、poll()以及登录记账。

后续各章所言及的“符合SUSv3规范”是指“符合XSI规范”。

> 由于POSIX和SUSv3目前由同一份文档描述，故而在文档的正文中，对于满足SUSv3符合度所需的额外接口和强制选项都以阴影和边注形式加以标明。

#### 未定义和未明确定义的接口

有时，我们会称某些接口在SUSv3中“未定义”或“未明确定义”。

未定义的接口是指尽管偶尔会在背景和原理描述中提及，却根本未经正式标准定义过的接口。

未明确定义的接口是指标准虽然包括了该接口，但却未对其重要细节进行规范。（通常是由于现有接口的实现差异导致标准委员会成员无法达成一致性意见。）

“未定义”或“未明确定义”的接口一经使用，在不同UNIX实现间移植应用就很难得到保证。尽管如此，少数此类接口在不同实现下的表现又相当一致。针对这些接口，本书通常会在提及时一一指出。

#### LEGACY（传统）特性

书中有时会指出SUSv3将某个特定特性标记为LEGACY。这一术语意味着保留此特性意在与老应用程序保持兼容，而在新应用程序中应避免使用。这也是标准对此特性的限制所在。大多数情况下，都能找到与LEGACY特性等效的其他API。

