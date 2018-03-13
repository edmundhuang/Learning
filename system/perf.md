# 性能优化
[Microsoft 操作系统 - 使用 perfmon 分析 Windows 性能](https://support.hpe.com/hpsc/doc/public/display?docId=emr_na-c01999716)  
使用perfmon分析Windows性能。

Windows平常在用的监控软件很多，不过内建的都有哪些呢?

众所皆知的Ctrl+Alt+Del叫出的Task Manager外，还有一个Windows内建的性能监控工具，叫做Performance Monitor 。

在开始-执行中输入perfmon即可，所有windows都有，包括XP。

Performance Monitor本身执行时，也会占用一定的系统资源，所以资源的使用量应该比实际的要稍微高一点。

这个工具在帮助管理员判断系统性能瓶颈时非常有用。

举个列子来说，任务管理器里显示CPU和内存的使用量都不高，但服务器的相应就是慢。 打开Performance Monitor，

让其运行一段时间后（因为参考平均值会比较准确），发现average disk queue的值比较高，这就说明物理服务器的硬盘负荷太重，

I/O操作的速度跟不上系统的要求。

CPU:

Processor Time：表示CPU的使用率，如果值大于80表示CPU的处理调度能力偏低。

硬盘：

Disk Time： 表示硬盘的I/O操作的频率（繁忙时间），如果值大于80表示硬盘I/O调度能力偏低。

Average Disk Queue Length：表示硬盘I/O操作等待队列的长度，如果值大于2表示硬盘I/O调度能力偏低。

内存

Pages/Sec： 表示系统对虚拟内存每秒钟的访问次数，如果值大于20表示有内存方面的问题。

NOTE: 有可能是物理内存偏低，也有可能是虚拟内存没有配置正确。一般情况下虚拟内存应为物理内存的1.5-2倍。
Committed Bytes 表示虚拟内存的大小，Available Bytes表示剩余可用内存的大小。

正常情况下，Available Bytes减少，pages（页面数）应该增加，提供页面交换。如果Available Bytes的值很小表示物理内存偏低。

当关闭一些应用以后，Committed Bytes应该减少，Available Bytes应该增加。

因为关闭的进程释放了之前占用的内存资源。如果相应的值没有发生变化，那么该进程就可能造成了内存泄漏。

Cache Bytes： 表示系统缓存的大小。如果值大于4M表示物理内存偏低。