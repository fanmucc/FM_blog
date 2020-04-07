#### node.js 单线程、非阻塞

##### 多线程与多线程

像`java`、`python`这个具有多线程的语言，多线程同步模式是这样的，将cpu分成几个线程，每个线程同步运行
![多线程](https://i.loli.net/2020/03/11/isp95B8rEaOHS12.png)

而`nodejs`采用单线程异步非阻塞模式，也就是说明一个计算独占cpu，遇到`I/O`请求不阻塞后面的计算，当`I/O`完成后，以事件的方式进行通知，继续执行计算2
![单线程](https://i.loli.net/2020/03/11/NroOM1eRXYxgmDT.png)

