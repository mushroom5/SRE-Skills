# Linux Command - lsof
lsof命令用于查看进程打开的文件，打开文件的进程，进程打开的端口（TCP、UDP）。找回/恢复删除的文件，是十分方便的系统监视工具。因为lsof命令需要访问核心内存和各种文件，需root用户。

**语法：**
`lsof (选项)`

**选项：**

```
-a：列出打开文件存在的进程；
-c<进程名>：列出指定进程所打开的文件；
-g：列出GID号进程详情；
-d<文件号>：列出占用该文件号的进程；
+d<目录>：列出目录下被打开的文件；
+D<目录>：递归列出目录下被打开的文件；
-n<目录>：列出使用NFS的文件；
-i<条件>：列出符合条件的进程。（4、6、协议、:端口、 @ip ）
-p<进程号>：列出指定进程号所打开的文件；
-u：列出UID号进程详情；
-h：显示帮助信息；
-v：显示版本信息。
```
**例子：**

```
lsof
command     PID USER   FD      type             DEVICE     SIZE       NODE NAME
init          1 root  cwd       DIR                8,2     4096          2 /
init          1 root  rtd       DIR                8,2     4096          2 /
init          1 root  txt       REG                8,2    43496    6121706 /sbin/init
init          1 root  mem       REG                8,2   143600    7823908 /lib64/ld-2.5.so
init          1 root  mem       REG                8,2  1722304    7823915 /lib64/libc-2.5.so
init          1 root  mem       REG                8,2    23360    7823919 /lib64/libdl-2.5.so
init          1 root  mem       REG                8,2    95464    7824116 /lib64/libselinux.so.1
init          1 root  mem       REG                8,2   247496    7823947 /lib64/libsepol.so.1
init          1 root   10u     FIFO               0,17                1233 /dev/initctl
migration     2 root  cwd       DIR                8,2     4096          2 /
migration     2 root  rtd       DIR                8,2     4096          2 /
migration     2 root  txt   unknown                                        /proc/2/exe
ksoftirqd     3 root  cwd       DIR                8,2     4096          2 /
ksoftirqd     3 root  rtd       DIR                8,2     4096          2 /
ksoftirqd     3 root  txt   unknown                                        /proc/3/exe
migration     4 root  cwd       DIR                8,2     4096          2 /
migration     4 root  rtd       DIR                8,2     4096          2 /
migration     4 root  txt   unknown                                        /proc/4/exe
ksoftirqd     5 root  cwd       DIR                8,2     4096          2 /
ksoftirqd     5 root  rtd       DIR                8,2     4096          2 /
ksoftirqd     5 root  txt   unknown                                        /proc/5/exe
events/0      6 root  cwd       DIR                8,2     4096          2 /
events/0      6 root  rtd       DIR                8,2     4096          2 /
events/0      6 root  txt   unknown                                        /proc/6/exe
events/1      7 root  cwd       DIR                8,2     4096          2 /
```
command:进程名称
PID: 进程标识符
PPID: 父进程标识符
USER: 进程所有者
PGUD: 进程所属组
FD： 文件描述符，应用程序通过文件描述符识别该文件
文件类型：

```
DIR：表示目录。
CHR：表示字符类型。
BLK：块设备类型。
UNIX： UNIX 域套接字。
FIFO：先进先出 (FIFO) 队列。
IPv4：网际协议 (IP) 套接字。
DEVICE：指定磁盘的名称
SIZE：文件的大小
NODE：索引节点（文件在磁盘上的标识）
NAME：打开文件的确切名称
```

**文件描述符：**

```
cwd：表示current work dirctory，即：应用程序的当前工作目录，这是该应用程序启动的目录，除非它本身对这个目录进行更改
txt：该类型的文件是程序代码，如应用程序二进制文件本身或共享库，如上列表中显示的 /sbin/init 程序
lnn：library references (AIX);
er：FD information error (see NAME column);
jld：jail directory (FreeBSD);
ltx：shared library text (code and data);
mxx ：hex memory-mapped type number xx.
m86：DOS Merge mapped file;
mem：memory-mapped file;
mmap：memory-mapped device;
pd：parent directory;
rtd：root directory;
tr：kernel trace file (OpenBSD);
v86  VP/ix mapped file;
0：表示标准输出
1：表示标准输入
2：表示标准错误

一般在标准输出、标准错误、标准输入后还跟着文件状态模式：
u：表示该文件被打开并处于读取/写入模式。
r：表示该文件被打开并处于只读模式。
w：表示该文件被打开并处于。
空格：表示该文件的状态模式为unknow，且没有锁定。
-：表示该文件的状态模式为unknow，且被锁定。

同时在文件状态模式后面，还跟着相关的锁：
N：for a Solaris NFS lock of unknown type;
r：for read lock on part of the file;
R：for a read lock on the entire file;
w：for a write lock on part of the file;（文件的部分写锁）
W：for a write lock on the entire file;（整个文件的写锁）
u：for a read and write lock of any length;
U：for a lock of unknown type;
x：for an SCO OpenServer Xenix lock on part      of the file;
X：for an SCO OpenServer Xenix lock on the      entire file;
space：if there is no lock.

```


