#### TCP连接的建立与终止

##### 三次握手

- TCP是面向连接的， 无论哪一方向向另一方发送数据之前, 都必须先在双方之间建立一条连接;
- 在TCP/IP协议中, TCP协议提供可靠的连接服务, 连接是通过三次握手进行初始化的;
- 三次握手的目的是同步连接双方的序列号和确认号并交换TCP窗口大小信息;

![三次握手示意图](https://user-gold-cdn.xitu.io/2017/8/10/6023cb46caf6ef8cdcc253cc9c827e40?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

###### 第一次握手

建立连接，客户端发送连接请求报文，将SYN位置为1, Sequence Number为X；然后，客户端进入SYN_SEND状态，等待服务器的确认；

###### 第二次握手

服务器接收到SYN报文段。服务器接收到客户端的SYN保人段，需要对这个报文段进行确认，设置Acknowledgment Number为x+1（Sequence Number +1); 同时，自己还要发送SYN请求信息，将SYN位置为1， Sequence Number为y；服务器端将上述所有信息放到一个报文段(既SYN + ACK报文段中)，一并发送给客户端， 此时服务器进入SYN_RECV状态；

###### 第三次握手

客户端受到服务器的SYN+ACK报文段，然后将Acknowledgment Number 设置为y+1，向服务器发送ACK宝报文段，这个报文段发送完毕之后，客户端和服务器端都进入ESTABLISHED状态, 完成TCP三次握手

##### 为什么要三次握手

为了防止已失效的连接请求报文段突然又传送到了服务端, 因而产生错误；

具体例子: "已失效的链接请求报文段"的产生在这样一种情况下: client 发出的第一次连接请求报文段并没有丢失, 而是在某个网络节点长时间滞留, 已致烟雾到连接释放以后的某个时间才到达server. 本来这事一个早已经失效的报文段， 但是 server 收到此失效的连接请求报文段后，就误认为是 client 再此发出的一个新的连接请求，浴室就像client发出确认报文段，同意建立连接。假设不采用"三次握手"，那么只要是sever发出确认，新的连接就建立了，由于现在client并没有发出建立连接的请求，因此不会理睬 server 的确认，也不会向 server 发送数据。但是server 却以为新的连接应建立，并一直保持连接等待client发送数据。这样， server很多资源就被白白浪费掉， 采用"三次握手"的办法可以防止上述现象的发生，例如刚刚的情况， client 不会向 server的确认发出确认。 server由于收不到确认，就知道client并没有要求建立连接；

##### 四次挥手

当客户端和服务器通过三次握手建立了TCP连接以后, 当数据传送完毕, 肯定是要断开TCP连接的，那对于TCP的断开连接, 这里就有了神秘的"四次分手"。

![四次挥手断开TCP连接](https://user-gold-cdn.xitu.io/2017/8/10/1fd63f511dd955e462bcdd3946e880bf?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

第一次挥手(分手): 主机1(可以是客户端也可是服务端)，设置Sequence Number， 向主机2发送一个FIN报文段，此时主机1进入FIN_WAIT_1状态，这表示主机1没有数据发送给主机2了；

第二次挥手(分手): 主机2收到主机1发送的FIN报文段，向主机1回一个ACK版web端， Acknowledgement Number 为 Squence Number + 1；主机1进入FIN_WAIT_2状态； 主机2告诉主机1， 我”同意“你的关闭请求；

第三次挥手(分手): 主机2向主机1发送FIN报文段，请求关闭连接，主机2进入 LAST_ACK 状态

第四次挥手(分手): 主机1收到主机2发送的FIN报文段， 向主机2发送ACK报文段，然后主机进入TIME_WAIT状态，主机2收到主机1的 ACK 报文段以后，就关闭连接，此时，主机1等待 2MSL 后依然没有收到回复， 则证明Server端已经正常关闭，那好，主机1也可以关闭连接了；

###### 为什么要四次分手

TCP协议是一种面向连接的、可靠的、基于字节流的运输层通信协议，TCP是全双工模式，这就意味着，当主机1发出FIN报文段时，只是表示主机1已经没有数据要发送了，主机1告诉主机2，它的数据已经全部发送完毕；但是，这个时候主机1还是可以接受来自主机2发送过来的数据，当主机2返回ACK报文段时，表示它已经知道主机1没有数据发送了，就会告诉主机1，我也没有数据要阿松了，之后主机1向主机2发送数据说"好的我们断开连接"，之后彼此就愉快的终端了这次TCP连接；

为什么要等待2MSL？

MSL: 报文段的最大生存事件，它是任何报文段被丢弃前在网络内最长时间

原因有二： 
1. 保证TCP协议的全双工连接能够可靠关闭；
2. 保证这次连接的重复数据段从网络中消失；

第一点: 如果主机1直接CLOSED了，那么由于IP协议的不可靠性或者是其他网络原因，导致主机2没有收到主机1最后回复的ACK。那么主机2就会在超时只有继续发送FIN，此时由于主机1已经CLOSED了，就找不到与重发的FIN对应的连接。所以，主机1不是直接进入CLOSED，而是要保持TIME_AIT, 当再次收到FIN的时候，能够保证对方收到ACK，最后正确的关闭连接

第二点: 如果主机1直接CLOSED，然后又再向主机2发起一个新连接，我们不能保证这个新连接与刚关闭的连接端口号是不同的，也就是说欧可能新连接和旧拦截的端口号是相同的，一般兰说不会发生什么问题，但是还是有特殊情况的出现：假设新连接和已经关闭的旧连接端口号是一样的，如果前一次连接的某些数据仍然滞留在网络中，这些延迟数据在建立新连接之后才到达主机2，由于新连接和旧连接端口号一致，TCP协议就会认为这些延迟数据是属于新连接的，这样就和真正的新连接数据包发生混淆，所以TCP连接还是要在TIME_WAIT状态等待2MSL，这样可以保证此次的所有数据都从网络中消失；