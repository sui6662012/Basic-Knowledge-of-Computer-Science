
* 本文主要内容为**刘超**老师在极客时间上的《趣谈网络协议》课程学习笔记

----

### 1. FTP（文件传输协议） 下载文件
> 采用两个 **TCP**连接传输一个文件

* 一 控制连接：服务器被动打开用于 FTP 的端口 21，客户端主动发起连接

* 二 数据连接： 每当一个文件在客户端和服务器之间传输的时候，就创建一个数据连接

**FTP 两种工作模式**

* 主动模式 PORT：
> 客户端随机打开一个 大于1024 的端口 N，向服务器的端口 21 发起连接； 同时开放 N+1 端口进行监听，向服务器发出 “port N+1”，服务器从自己的数据端口20 主动连接到客户端的端口 N+1

* 被动模式 PASV：
> 开启一个 FTP 连接， 客户端打开两个任意的 本地端口 N和 N+ 1 (大于 1024)。 第一个端口连接服务器的 21 端口，提交 PASV命令。 服务器会开启一个任意端口 P（大于 1024），返回 “227 entering passive mode”消息，包含FTP开放数据传输的端口。 之后客户端的 N+1号端口会连接到服务器的端口 P，端口之间进行数据传输。

----

### 2. P2P peer-to-peer
> 资源不是集中在某些设备上，而是分散在储存在多台设备上。设备可以称为 peer

* 下载文件的时候，只需要得到存在文件的 peer，并和 peer 之间建立点对点的连接（不需要到中心服务器上面），就可以就近下载文件

* 下载文件之后，也变成了 peer 中的一员， 也可以给别人提供下载

---

### 3. 种子文件 .torrent

**如何知道哪些peer 有文件是一个关键问题**

#### 1. 种子文件简介

* 文件由 两部分组成 ： announce（tracker URL） 和 文件信息

* 文件信息中 包含：
	* Info 区： 说明种子有几个文件，文件多大， 目录结构，以及目录和文件的名字。
	* Name 字段： 制定顶层目录的名字
	* 每个段的大小 ： BitTorrent （BT） 协议，把文件分成很多个小段，然后分段下载
	* 段哈希值 ： 将整个种子中，每个段 SHA-1 哈希值拼在一起

#### 2. 下载 过程

1.  BT 客户端 解析 .torrent 文件，得到 tracker地址，连接成、tracker服务器。

2. tracker服务器将其他下载这的 IP提供给 下载的人，

3. 下载者连接其他的下载者，根据 .torrent 文件，两者分别告知对方已经有的块，然后交换对方没有的数据

#### 3. tracker

* tracker 需要收集下载者的信息，并将信息提供给其他的下载者

* 下载的过程是去中心化的，但是加入 P2P 的网络还是需要借助 **tracker 中心服务器**

----

### 4. 去中心化网络 DHT -- Distributed Hash Table
> 每个加入 DHT网络的人，都要负责储存网络里面的资源和其他成员的联系信息

**暂留**







































