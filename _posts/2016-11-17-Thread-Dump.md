---
layout: post
title: threadDump分析
categories: [programming]
tags:
- java jvm thread
---

```
 kill -9 pid
```
or
```
 sudo jstack -l 1099 | tee -a jstack.log
```
1099: Unable to open socket file: target process not responding or HotSpot VM not loaded
The -F option can be used when the target process is not responding

[参考链接](https://my.oschina.net/dabird/blog/691692)
