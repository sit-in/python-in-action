# 高性能编程

串行：任务A执行结束才能开始执行B，单个线程只能执行一个任务

并发：允许我们在等待一个I/O操作完成的时候执行其他操作，从而帮助我们这个浪费的时间利用起来。（有多个处理任务的能力不一定要同时）

并行：并行在于「同时」处理多个任务的能力。（吃饭接电话）

![](/assets/串行和并行对比.png)

1. 多线程

2. 多进程

3. Gevent，tornado，ayncio

4. golang，nodejs 异步方式 [https://time.geekbang.org/column/article/693](https://time.geekbang.org/column/article/693)  

5. 爬虫

## 多线程

讨论 Python 程序的效率时，经常提到的弊端之-是全局解释器锁（Global Interpreter Lock, GIL\), GIL 限制任何时间都仅有一个线程在执行。但是存在即合理，由于线程是轻量级的，并且相互之间易于通信，GIl 保护了所有全局的解释器和环境状态变量。如果不使用 GIL 会带来了包括死锁、争用条件和高复杂性在内的各种问题。那么由于 GIL 的限制，使用多线程就完全没有意义了吗？其实不是的，原因如下：

1. Python 大部分是使用 C 语言编写的，一些标准库和第三方的模块也是用 C 编写的，而 C 语言代码是可以获取和释放 GIL 的，这在一定程度上缓解了 GIL 的问题。一些重要的、需要更高运行效率的模块还可以使用 C 语言编写，这样就可以利用更多的 CPU资源。

   1. 多线程适合解决由于网络、磁盘等资源造成的I1 O阻塞问题，它利用了等待1/O 请求完成被阻塞而导致的 CPU 空闲时间。计算密集型的工作不适合使用多线程完成，因为计算需要 CPU 资源，如果 CPU 繁忙的话，使用多线程并没有更多地利用 CPU 空闲时间，反而由于 CPU 需要额外调度多线程，以及线程切换的各种开销，多线程的运行效率比单线程还要慢。

ps: 多线程在 CPU密集型 GIL竞争 导致速度更慢（多线程单核没有GIL竞争）

## 多进程

使用进程代替线程可以有效避开 GIL，因为每个进程都拥有自己的 Python 解释器实例，也就不受 GIL 的限制了。计算密集型的任务通常应该使用多进程方式，也就是使用 multiprocessing 模块。multiprocessing 模块允许程序充分利用多处理器，并可以跨平台使用。 I/O密集型的任务瓶颈主要在网络延迟，所以使用多线程或者多进程都可以。

利用多核CPU达到更高效速度

ps : 超线程技术30%效果，建议增加更多CPU

## 异步对比

异步编程：限制请求的链接数，过多会导致CPU上下文切换过于频繁，过少会导致IO等待时间过长

grequests = gevent + requests

串行requests爬虫和并行爬虫grequests区别（100并发 70倍看机器性能）

> resp\_futures = \(grequests.get\(u\) for u in urls\)
>
> resp = grequests.imap\(rese\_futreues, size=100\)

Tornado： 1.  事件循环全局时间 2. 更智能进行分配资源和复用链接（内建立100并发信号量）

Gevent：   1. 事件循环在iwait 函数才运行 2. 自己控制调整

Asyncio： 1. 更底层 yield from （不需要通过raise来进行返回值）同Gevent通过信号量进行限制请求数

例子：IO密集+CPU密集 ==》 多进程来处理IO，避免影响CPU计算

计算数据是否是素数并且存入数据库：

![](/assets/io_nonio.png)

## 爬虫

1. 使用代理
2. 伪造UA，每次请求随机生成 fake-useragent
3. 使用Referfer
4. 解析HTML，BeautifulSoup，html.parser，lxml，html5lib

其他：

1. \[Python进阶：聊聊IO密集型任务、计算密集型任务，以及多线程、多进程\]\([https://zhuanlan.zhihu.com/p/24283040\](https://zhuanlan.zhihu.com/p/24283040%29\)
2. 安全规范 参考confluence



