#volatile作用,以及对指令重排序的影响
> 1.volatile轻量级同步机制 保证了`变量`内存的可见性 
> 2.保证JVM遵循`内存屏障`的约束,依靠内存屏障`阻止指令重排序`
## 指令重排序
> 指令重排的目的是为了在`不改变单线程`程序执行结果的前提下，优化程序的运行效率。
> 虽然优化了程序的执行效率，但是在某些情况下，会影响到多线程的执行结果。
##内存屏障
>内存屏障也称为内存栅栏或栅栏指令，是一种屏障指令，它使CPU或编译器对屏障指令之前和之后发出的内存操作执行一个排序约束。通俗来讲内存屏障是保证了CPU指令的先入先执行
内存屏障共分为四种类型：
###LoadLoad屏障：
抽象场景：Load1; LoadLoad; Load2
Load1 和 Load2 代表两条读取指令。在Load2要读取的数据被访问前，保证Load1要读取的数据被读取完毕。
###StoreStore屏障：
抽象场景：Store1; StoreStore; Store2
Store1 和 Store2代表两条写入指令。在Store2写入执行前，保证Store1的写入操作对其它处理器可见
###LoadStore屏障：
抽象场景：Load1; LoadStore; Store2
在Store2被写入前，保证Load1要读取的数据被读取完毕。
###StoreLoad屏障：
抽象场景：Store1; StoreLoad; Load2
在Load2读取操作执行前，保证Store1的写入对所有处理器可见。StoreLoad屏障的开销是四种屏障中最大的。



在一个变量被volatile修饰后，JVM会为我们做两件事：
1.在每个volatile写操作前插入StoreStore屏障，在写操作后插入StoreLoad屏障。
2.在每个volatile读操作前插入LoadLoad屏障，在读操作后插入LoadStore屏障。