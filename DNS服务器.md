# DNS服务器
## 前景知识
### 配置文件
/etc/hosts: 最早的Hostname对应IP的文件
/etc/resolv.conf: DNS服务器IP记录处
/etc/nsswitch.conf: 这个文件决定先使用`/etc/hosts` 还是`/etc/resolv.conf`的设置

```
>>>vim /etc/nsswitch.conf
hosts:      files dns
#files 就是 /etc/hosts
#dns 就是 /etc/resolv.conf
#一般情况下，Linux的默认主机名与IP的对应解析都以/etc/hosts优先
```

### FQDN（Fully Qualified Domain Name）完整主机名
由 `主机名和域名` 组成的叫完整主机名

###DNS & Bind
DNS：一种因特网的通信协议名称
BIND：提供DNS服务的软件

### DNS阶层架构
![](/Users/user/MyGit/SRE-Skills/Images/DNS阶层架构图.png)
![](https://github.com/mushroom5/SRE-Skills/tree/master/Images/DNS阶层架构图.png)
最上方的`.`是root DNS服务器，管理以组织、国家为分类的第二层主机名，这两者称为TLDs（Top Level Domains）
一般顶级域名（Generic TLDs，gTLD）：.com、.org、.gov等
地区顶级层域名（Country Code TLDs，ccTLD）：.uk、.jp、.cn等

### 通过DNS查询主机名IP的流程
![](/Users/user/MyGit/SRE-Skills/Images/DNS查询流程.png)
![](https://github.com/mushroom5/SRE-Skills/tree/master/Images/DNS查询流程.png)
首先，当你在浏览器的网址列输入 http://www.ksu.edu.tw 时，你的计算机就会依据相关设定 (在 Linux 底下就是利用 /etc/resolv.conf 这个档案) 所提供的 DNS的 IP 去进行联机查询了。由于目前最常见的 DNS 服务器就属 Hinet 的 168.95.1.1这个 DNS，所以我们就拿他来做例子 hinet 的这部服务器会这样工作：
 
1. 收到用户的查询要求，先查看本身有没有纪录，若无则向 . 查询：由于 DNS 是阶层式的架构，每部主机都会管理自己辖下的主机名解译而已。因为 hinet 并没有管理台湾学术网络的权力， 因此就无法直接回报给客户端。此时 168.95.1.1 就会向最顶层，也就是 . (root) 的服务器查询相关 IP 信息。
 
2. 向最顶层的 . (root) 查询：168.95.1.1 会主动的向 . 询问 www.ksu.edu.tw 在哪里呢？但是由于 . 只记录了 .tw 的信息 (因为台湾只有 .tw 向 . 注册而已)，此时 . 会告知『我是不知道这部主机的 IP 啦，不过，你应该向 .tw 去询问才对，我这里不管！ 我跟你说 .tw 在哪里吧！』
 
3. 向第二层的 .tw 服务器查询：168.95.1.1 接着又到 .tw 去查询，而该部机器管理的又仅有 .edu.tw, .com.tw, gov.tw... 那几部主机，经过比对后发现我们要的是 .edu.tw 的网域，所以这个时候 .tw 又告诉 168.95.1.1 说：『你要去管理 .edu.tw 这个网域的主机那里查询，我有他的 IP ！』
 
4. 向第三层的 .edu.tw 服务器查询：同理可证， .edu.tw 只会告诉 168.95.1.1 ，应该要去 .ksu.edu.tw 进行查询，这里只能告知 .ksu.edu.tw 的 IP 而已。
 
5. 向第四层的 .ksu.edu.tw 服务器查询：等到 168.95.1.1 找到 .ksu.edu.tw 之后， .ksu.edu.tw 说：『没错！这部主机名是我管理的～ 我跟你说他的 IP 是...所以此时 168.95.1.1 就能够查到 www.ksu.edu.tw 的 IP 啰！
 
6. 记录暂存内存并回报用户：
查到了正确的 IP 后， 168.95.1.1 的 DNS 机器总不会在下次有人查询www.ksu.edu.tw 的时候再跑一次这样的流程吧！ 很远很累的！而且也很耗系统的资源与网络的带宽，所以呢， 168.95.1.1 这个 DNS 会很聪明的先记录一份查询的结果在自己的暂存内存当中，以方便响应下一次的相同要求啊！ 最后则将结果回报给 client 端！当然啦，那个记忆在 cache 当中的数据，其实是有时间性的，当过了 DNS 设定记忆的时间 (通常可能是 24 小时)，那么该记录就会被释放喔！
 
整个分层查询的流程就是这样，总是得要先经过 `. `根来向下一层进行查询，最终总是能得到答案的。

```
Q:从在浏览器里输入域名到返回结果，中间都做了什么事情？
A:
```

### DNS 使用的port number
TCP & UDP：53 端口
可在/etc/services文件中搜寻domain关键字查看
通常DNS是以UDP这个较快速的数据传输协议查询的，万一没有办法查找到完整的信息时，会再次以TCP协议重新查询。

### DNS数据库的记录：正解、反解、Zone
从主机名查询到IP的流程称为：正解
从IP反解析到主机名的流程称为：反解
无论正解、反解，每个域的记录就是一个区域（Zone）
#### 正解
SOA：（Start of Authority）
NS：（Name Server），记录的数据是DNS服务器
A：（Address），记录的是IP的对应
#### 反解
PTR：（PointTeR），记录的数据是反解到主机名
#### 每台DNS都需要的正解Zone：hint
hint:根目录在哪里的记录
所以说，一部简单的正解 DNS 服务器，基本上就要有两个 zone 才行，一个是hint ，一个是关于自己领域的正解 zone。
### DNS 数据库的类型：hint、Master/Slave架构
hint：.(root)基本数据库类型；
master，slave 是两种基本类型，用来解决DNS服务器主从结构，数据同步问题的。
 
**master：**
要管理员自己手动去修改与设定;并且重启后才生效；
一般来说，我们说的DNS设定，就是指设定这种数据库的类型
给slave的DNS提供数据库内容
 
**slave：**
必须与master相互搭配
只支持一主多从
更改master之后，slave自动更新
 
**master/slave的查询优先权？**
在 DNS 系统当中，领域名的查询是『先抢先赢』的状态；
 
 
**Master / Slave 数据的同步化过程：**
基本上，不论 Master 还是 Slave 的数据库，都会有一个代表该数据库新旧的『序号』，这个序号数值的大小，是会影响是否要更新的动作。
 
**更新的两种方式：**
**master主动告知**
 Master 在修改了数据库内容，并且加大数据库序号后， 重新启动 DNS 服务，那 master 会主动告知 slave 来更新数据库，
**slave主动提出**
Slave 会定时的向 Master 察看数据库的序号， 当发现 Master 数据库的序号比 Slave 自己的序号还要大 (代表比较新)，那么 Slave 就会开始更新

-------

## DNS服务器搭建
### 软件
BIND（Berkeley Internet Name Domain）

```
>>>rpm -qa | grep '^bind'
bind-libs-9.8.2-0.68.rc1.el6_10.1.x86_64  给bind与相关命令使用的函数库
bind-9.8.2-0.68.rc1.el6_10.1.x86_64  bind主程序所需软件
bind-utils-9.8.2-0.68.rc1.el6_10.1.x86_64  客户端查找主机名的相关命令
bind-chroot-9.8.2-0.68.rc1.el6_10.1.x86_64  将bind主程序关在家里面
```








