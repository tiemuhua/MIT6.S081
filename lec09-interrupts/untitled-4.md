# Untitled

在我们向console输出字符时，如果发生了中断，RISC-V会做什么操作？我们之前已经在SSTATUS寄存器中打开了中断，所以处理器会被中断。假设键盘生成了一个中断并且发向了PLIC，PLIC将中断路由给了我一个特定的CPU核，并且这个CPU核设置了SIE寄存器的bit（注，针对外部中断的E bit位），那么会发生以下事情：

* 首先，程序会删除SIE寄存器相应的bit，这样可以阻止CPU核被其他中断打扰，该CPU核可以专心处理当前中断。处理完成之后，可以再次设置SIE寄存器相应的bit。
* 之后，程序会设置SEPC寄存器为当前的程序计数器。我们假设Shell正在用户空间运行，突然来了一个中断，那么当前Shell的程序计数器会被保存。
* 之后，程序要保存当前的mode。
