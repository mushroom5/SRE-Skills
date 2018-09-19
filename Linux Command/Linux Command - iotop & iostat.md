# Linux Command - iotop & iostat
### **iotop:**
iotop命令是用来监视磁盘I/O使用状况的top类工具。可以查看到每个进程使用IO的情况。

```
Total DISK READ: 0.00 B/s | Total DISK WRITE: 114.33 M/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND
30266 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.09 % [flush-8:16]
 1613 be/3 root        0.00 B/s    0.00 B/s  0.00 %  0.01 % [jbd2/sda1-8]
34467 be/4 work        0.00 B/s  167.18 K/s  0.00 %  0.00 % java -Xms32g -Xmx32g -XX:+UseConcMarkSweepGC -XX:CMSInitiatingOccupancyFraction=75 -XX:+UseCMSInitiating~r/local/elasticsearch/config -cp /usr/local/elasticsearch/lib/* org.elasticsearch.bootstrap.Elasticsearch
34641 be/4 work        0.00 B/s  159.91 K/s  0.00 %  0.00 % java -Xms32g -Xmx32g -XX:+UseConcMarkSweepGC -XX:CMSInitiatingOccupancyFraction=75 -XX:+UseCMSInitiating~r/local/elasticsearch/config -cp /usr/local/elasticsearch/lib/* org.elasticsearch.bootstrap.Elasticsearch
85.35 be/4 work        0.00 B/s  156.94 K/s  0.00 %  0.00 % java -Xms32g -Xmx32g -XX:+UseConcMarkSweepGC -XX:CMSInitiatingOccupancyFraction=75 -XX:+UseCMSInitiating~r/local/elasticsearch/config -cp /usr/local/elasticsearch/lib/* org.elasticsearch.bootstrap.Elasticsearch
```

**安装：**
` yum install iotop `


```
wget http://guichaz.free.fr/iotop/files/iotop-0.4.4.tar.gz    
tar zxf iotop-0.4.4.tar.gz    
python setup.py build    
python setup.py install 
```

**语法：**
`iotop（选项）`

**选项：**

```
-o：只显示有io操作的进程
-b：批量显示，无交互，主要用作记录到文件。
-n NUM：显示NUM次，主要用于非交互式模式。
-d SEC：间隔SEC秒显示一次。
-p PID：监控的进程pid。
-u USER：监控的进程用户。
```
**快捷键：**

```
左右箭头：改变排序方式，默认是按IO排序。
r：改变排序顺序。
o：只显示有IO输出的进程。
p：进程/线程的显示方式的切换。
a：显示累积使用量。
q：退出。
```

### **iostat:**
iostat被用于监视系统输入输出设备和cpu的使用情况。
特点：汇报磁盘活动统计情况、cpu使用情况。
缺点：不能针对某个进程进行深入分析，仅对系统的整体情况进行分析。

**语法：**
`iostat (选项) （参数）`

**选项：**

```
-c：仅显示CPU使用情况；
-d：仅显示设备利用率；
-k：显示状态以千字节每秒为单位，而不使用块每秒；
-m：显示状态以兆字节每秒为单位；
-p：仅显示块设备和所有被使用的其他分区的状态；
-t：显示每个报告产生时的时间；
-V：显示版号并退出；
-x：显示扩展状态
```
**参数：**

```
间隔时间：每次报告的间隔时间（秒）；
次数：显示报告的次数。
```
**例子：**

```
[root@hostname ~]# iostat -x 1 10 /dev/sda
Linux 2.6.32-358.el6.x86_64 (hostname) 	09/19/2018 	_x86_64_	(40 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           4.22    0.00    0.55    0.44    0.00   94.79

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.09    48.05    4.35    3.11   227.85   409.30    85.34     0.01    0.89   0.22   0.17
sdb               1.29     5.84  132.41  664.17 11429.24 33350.92    56.22     0.11    0.13   0.17  13.20

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          18.70    0.00    1.23    0.08    0.00   80.00

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     2.00    1.00    2.00    16.00    32.00    16.00     0.00    0.33   0.33   0.10
sdb               0.00     0.00   35.00    0.00  1752.00     0.00    50.06     0.06    1.69   1.34   4.70

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           9.41    0.00    0.78    0.00    0.00   89.82

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
sdb               0.00     0.00   12.00  113.00    96.00 40544.00   325.12     0.50    3.98   0.12   1.50

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           3.99    0.00    0.43    0.00    0.00   95.59

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     2.00    0.00    2.00     0.00    32.00    16.00     0.00    0.00   0.00   0.00
sdb               0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          25.12    0.00    1.20    0.00    0.00   73.68

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     0.00    0.00    1.00     0.00     8.00     8.00     0.00    3.00   3.00   0.30
sdb               0.00     0.00   30.00    0.00   304.00     0.00    10.13     0.04    1.17   1.17   3.50

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          19.25    0.00    0.60    0.00    0.00   80.15

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
sdb               0.00     0.00    4.00    0.00    32.00     0.00     8.00     0.00    0.25   0.25   0.10

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          10.15    0.00    1.03    0.45    0.00   88.37

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     0.00   21.00    0.00  1864.00     0.00    88.76     0.03    1.24   0.52   1.10
sdb               0.00    19.00  821.00  232.00 58056.00  4728.00    59.62     0.59    0.56   0.19  20.00

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           9.28    0.00    0.65    0.33    0.00   89.74

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
sdb               0.00     1.00  519.00  182.00 37944.00 59120.00   138.47     0.66    0.90   0.29  20.30

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           5.22    0.00    0.68    1.83    0.00   92.27

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
sdb               3.00   212.00 2325.00  831.00 229448.00 13608.00    77.01     8.36    2.66   0.24  75.30

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          11.88    0.00    0.93    1.88    0.00   85.31

Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await  svctm  %util
sda               0.00     6.00   20.00    6.00  1800.00    96.00    72.92     0.03    1.31   0.73   1.90
sdb               0.00     0.00   53.00    0.00   696.00     0.00    13.13     0.14    2.55   1.49   7.90
```
第二行: 系统信息、监测时间
第三行 ~ 第四行: CPU使用情况
其余: I/O输出信息：

| 标示 | 说明 |
| --- | --- |
| Device | 监测设备名称 |
| rrqm/s | 每秒需要读取需求的数量 |
| wrqm/s | 每秒需要写入需求的数量 |
| r/s  | 每秒实际读取需求的数量 |
| w/s | 每秒实际写入需求的数量 |
| rsec/s | 每秒读取区段的数量 |
| wsec/s | 每秒写入区段的数量 |
| rkB/s | 每秒实际读取的大小，单位为KB |
| wkB/s | 每秒实际写入的大小，单位为KB |
| avgrq-sz | 需求的平均大小区段 |
| avgqu-sz | 需求的平均队列长度 |
| await | 等待I/O平均的时间（milliseconds） |
| svctm | I/O需求完成的平均时间 |
| %util | 被I/O需求消耗的CPU百分比 |








