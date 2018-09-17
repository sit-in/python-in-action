# 高性能编程

并发：允许我们在等待一个I/O操作完成的时候执行其他操作，从而帮助我们这个浪费的时间利用起来。

并行：

异步编程：限制请求的链接数，过多会导致CPU上下文切换过于频繁，过少会导致IO等待时间过长

grequests = gevent + requests

串行requests爬虫和并行爬虫grequests区别（100并发 70倍看机器性能）

> resp\_futures = \(grequests.get\(u\) for u in urls\)
>
> resp = grequests.imap\(rese\_futreues, size=100\)

Tornado：1.  事件循环全局时间 2. 更智能进行分配资源和复用链接（内建立100并发信号量）

Gevent：1. 事件循环在iwait 函数才运行 2. 自己控制调整

Asyncio： 1. 更底层 yield from （不需要通过raise来进行返回值）同Gevent通过信号量进行限制请求数

IO密集+CPU密集 ==》 多进程来处理IO，避免影响CPU计算

![](/assets/io_nonio.png)

1. 多线程

2. 多进程

3. Gevent，tornado，ayncio

4. golang，nodejs对比

5. 爬虫

## 多线程

![](/assets/compare.png)

## 多进程

## 异步对比

## 爬虫

1. 使用代理
2. 伪造UA，每次请求随机生成 fake-useragent
3. 使用Referfer
4. 解析HTML，BeautifulSoup，html.parser，lxml，html5lib



