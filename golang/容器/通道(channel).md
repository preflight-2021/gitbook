# channel

channel是Golang在语言层面提供的goroutine间的通信方式，比Unix管道更易用也更轻便。channel主要用于进程内各goroutine间通信。

# chan数据结构

src/runtime/chan.go:hchan 定义了channel的数据结构：

```
type hchan struct {
	qcount   uint           // 当前队列中剩余元素个数;
	dataqsiz uint           // 环形队列长度，即可以存放的元素个数;
	buf      unsafe.Pointer // 环形队列指针;
	elemsize uint16         // 每个元素的大小;
	closed   uint32         // 标识关闭状态;
	elemtype *_type         // 元素类型;
	sendx    uint           // 队列下标，指示元素写入时存放到队列中的位置;
	recvx    uint           // 队列下标，指示元素从队列的该位置读出;
	recvq    waitq          // 等待读消息的goroutine队列;
	sendq    waitq          // 等待写消息的goroutine队列;
	lock     mutex          // 互斥锁，chan不允许并发读写;
}
```

# 环形队列

chan内部实现了一个环形队列作为其缓冲区，队列的长度是创建chan时指定的。

从channel读数据，如果channel缓冲区为空或者没有缓冲区，当前goroutine会被阻塞。向channel写数据，如果channel缓冲区已满或者没有缓冲区，当前goroutine会被阻塞。

被阻塞的goroutine将会挂在channel的等待队列中：

- 因读阻塞的goroutine会被向channel写入数据的goroutine唤醒；
- 因写阻塞的goroutine会被从channel读数据的goroutine唤醒；

注意，一般情况下recvq和sendq至少有一个为空。只有一个例外，那就是同一个goroutine使用select语句向channel一边写数据，一边读数据。

# channel读写

### 创建channel

创建channel的伪代码如下所示：

```golang
func makechan(t *chantype, size int) *hchan {
	var c *hchan
	c = new(hchan)
	c.buf = malloc(元素类型大小 * size)
	c.elemsize = 元素类型大小
	c.elemtype = 元素类型
	c.dataqsiz = size
	return c
}
```



### 向channel写数据

1. 如果等待接收队列recvq不为空，说明缓冲区中没有数据或者没有缓冲区，此时直接从recvq取出G,并把数据写入，最后把该G唤醒，结束发送过程；
2. 如果缓冲区中有空余位置，将数据写入缓冲区，结束发送过程；
3. 如果缓冲区中没有空余位置，将待发送数据写入G，将当前G加入sendq，进入睡眠，等待被读goroutine唤醒。

### 从channel读数据

1. 如果等待发送队列sendq不为空，且没有缓冲区，直接从sendq中取出G，把G中数据读出，最后把G唤醒，结束读取过程；
2. 如果等待发送队列sendq不为空，此时说明缓冲区已满，从缓冲区中首部读出数据，把G中数据写入缓冲区尾部，把G唤醒，结束读取过程；
3. 如果缓冲区中有数据，则从缓冲区取出数据，结束读取过程；
4. 将当前goroutine加入recvq，进入睡眠，等待被写goroutine唤醒。

### 关闭channel

关闭channel时会把recvq中的G全部唤醒，本该写入G的数据位置为nil。把sendq中的G全部唤醒，但这些G会panic。

除此之外，panic出现的常见场景还有：

1. 关闭值为nil的channel
2. 关闭已经被关闭的channel
3. 向已经关闭的channel写数据