---
layout: post
title: 线上CPU过高-threadDump分析
categories: [programming]
tags:
- java jvm thread


#问题现象
一台机器的cpu过高
首先想到是dump线上thread日志


kiil -3 PID ，默认会出输出到catalina.out日志里
```
 kill -3 389
```
or 可以指定日志输出
```
 sudo jstack -l 389 | tee -a jstack.log
```
出现以下异常 用-F替代

1099: Unable to open socket file: target process not responding or HotSpot VM not loaded
The -F option can be used when the target process is not responding

可以使用以上任意命令，一定多运行几遍获取数据。

然后使用 top -ac -H 获取到cpu最高的线程pid，计算器转为16进制，在文件里搜索


#问题分析
## 日志

出现了非常频繁的ParallelGC日志
```
"GC task thread#0 (ParallelGC)" prio=10 tid=0x00007fb428021800 nid=0x263d runnable 

"GC task thread#1 (ParallelGC)" prio=10 tid=0x00007fb428023000 nid=0x263e runnable 

"GC task thread#2 (ParallelGC)" prio=10 tid=0x00007fb428025000 nid=0x263f runnable 

"GC task thread#3 (ParallelGC)" prio=10 tid=0x00007fb428027000 nid=0x2640 runnable 
```

出现次数非常多的RUNABLE状态的业务日志
```
"http-8000-10" daemon prio=10 tid=0x00007fb3f8025000 nid=0x276c runnable [0x00007fb398c82000]
   java.lang.Thread.State: RUNNABLE
   ...
   ArAccrualDetailServiceImpl.queryByIds
   ...
  
```

jstat监控GC：
```
[l-qreaper.dev.cn0 ~]$ sudo jstat -gccause 29781 1000
  S0     S1     E      O      P     YGC     YGCT    FGC    FGCT     GCT    LGCC                 GCC                 
 75.48   0.00  53.94  93.55  35.02    504   37.875   121  287.080  324.955 Allocation Failure   No GC               
  0.00  66.57  96.87  95.04  35.02    505   38.002   121  287.080  325.081 Allocation Failure   No GC               
  0.00  54.69   0.00  98.51  35.02    507   38.214   122  287.080  325.294 Allocation Failure   Ergonomics          
  0.00  54.69   0.00  98.51  35.02    507   38.214   122  287.080  325.294 Allocation Failure   Ergonomics          
  0.00  54.69   0.00  98.51  35.02    507   38.214   122  287.080  325.294 Allocation Failure   Ergonomics          
  0.00  54.69   0.00  98.51  35.02    507   38.214   122  287.080  325.294 Allocation Failure   Ergonomics          
  0.00  21.30 100.00  99.99  35.01    507   38.214   123  290.270  328.484 Allocation Failure   Ergonomics          
  0.00  21.30 100.00  99.99  35.01    507   38.214   123  290.270  328.484 Allocation Failure   Ergonomics          
  0.00  21.30 100.00  99.99  35.01    507   38.214   123  290.270  328.484 Allocation Failure   Ergonomics          
  0.00  21.30 100.00  99.99  35.01    507   38.214   123  290.270  328.484 Allocation Failure   Ergonomics          
  0.00   0.00 100.00 100.00  35.01    507   38.214   124  293.612  331.826 Allocation Failure   Ergonomics          
  0.00   0.00 100.00 100.00  35.01    507   38.214   124  293.612  331.826 Allocation Failure   Ergonomics          
  0.00   0.00 100.00 100.00  35.01    507   38.214   124  293.612  331.826 Allocation Failure   Ergonomics          
  0.00   0.00 100.00 100.00  35.01    507   38.214   124  293.612  331.826 Allocation Failure   Ergonomics        
```
可以看到youngGc非常频繁，我设置的是每秒监控一次


#调优
很详细
(http://www.importnew.com/22336.html)

#参考：

GC专家系列目录索引(推荐阅读)
(https://segmentfault.com/a/1190000004369048)

堆内存分配(GC算法逻辑)：
(http://www.blogjava.net/fancydeepin/archive/2013/09/29/jvm_heep.html)
官方
(http://www.oracle.com/technetwork/java/javase/tech/vmoptions-jsp-140102.html)


[https://my.oschina.net/dabird/blog/691692]
[http://blog.csdn.net/rachel_luo/article/details/8920596]



