### 2.3.2　NAND型闪存

NAND型闪存使用一种相对较新的闪存技术。当NAND型闪存投放市场时，前一节介绍的传统闪存就被称为了NOR型闪存。它们之间的区别与闪存存储单元的内部架构有关。NAND型闪存设备通过提供更小的块尺寸改进了传统（NOR型）闪存的一些限制，它可以更快更有效地进行写操作，同时大大提高了闪存阵列的使用效率。

NOR型闪存为微处理器提供的接口方式与很多微处理器外围设备的做法类似。也就是说，它们有并行的数据和地址总线，直接<a class="my_markdown" href="['#anchor029']"><sup class="my_markdown">[9]</sup></a>连接到微处理器的数据/地址总线上。闪存阵列的每个字节或字（word）可以随机寻址。相反，NAND型闪存设备是通过复杂的接口串行访问的，而且这些接口因厂商而异。NAND型闪存设备的操作模式更类似于传统的硬盘驱动器加上附带的控制器。数据是以串行突发（burst）方式访问的，每次突发访问的数据量远远小于NAND型闪存的块大小。相比于NOR型闪存，虽然NAND型闪存的写入时间要少很多，但其写寿命却比NOR型闪存高出一个数量级。

<a class="my_markdown" href="['#ac029']">[9]</a>　这里的直接是逻辑上的概念。实际的电路有可能会包含总线缓存（bus buffer）或桥接（bridge）设备等。

总的来说，NOR型闪存可以被微处理器直接访问，甚至于代码可以直接在NOR型闪存中执行。（然而，因为性能方面的原因，很少有人这样做，除非系统资源极其匮乏。）实际上，很多处理器都不能像对待DRAM一样缓存（cache）访问闪存的指令。这进一步降低了代码的执行速度。相反，NAND型闪存更适合于以文件系统的格式大容量存储数据，而不是撇开文件系统，直接存储二进制可执行代码和数据。

