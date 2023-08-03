---
layout: post
title: 一个简单的脚本来启动/停止服务
categories: shell
---

一个简单的脚本来启动/停止服务
=====================
  
  在开发调试一个调试一个应用的时候需要经常重启服务，这时多打几个字符的命令打多了也会觉得麻烦，想执行越简单越好。我们可以写一个脚本来自动化这一过程，重启过程包括启动和停止，下面来分别介绍一下。
  
# 启动服务
  
  如果服务是个守护进程，直接command xxx就行了，比较好处理。如果不是就要做相应的处理，以启动web.py的服务为例，main写在webmain.py里面,此时命令为为
  

```shell  
  python webmain.py
``` 
  
  但是这样的话，终端会一直挂起，不能再回到标准输入里面，此时需要在后面加上 &
  
```shell  
  python webmain.py &
``` 

 此时会遇到几个问题，如下的问题
 
* 退出shell的时候服务就会挂掉
* 过程中的一些输出直接就输出到控制台上(试过很多方法都不行) 
  
  我们可以通过nohub命令来解决这个问题，它默认将信息打印到nohub.out中

```shell  
  nohub python webmain.py &
``` 
 
  当然我们可以将它重定向到某个文件，并将标准错误输出也合在一起，所以启动脚本start.sh包含像这个样子的：
  
```shell  
  #...
  nohub python webmain.py > file 2>&1 &
``` 

# 停止服务
  一般我们会使用kill命令停止进程来停止服务，一个简单暴力的方法就是kill -9 xxx
  
1. 通过ps -ef来获取所有进程
2. 通过grep 来过滤指定关键字，用grep -v来过滤不包含某个关键字(因为在使用grep或其他命令的时候会多起一些其他的进程)
3. 通过awk来获取对应列的值
  
  所以停止脚本start.sh像这个样子的：
  
```shell  
  #...
  stop()
  {
    pid=`ps -ef | grep ${app} | grep -v grep| awk '{print $2}'`
    if [ ! -z "$pid" ]; then
      kill -9 $pid;
    fi
  }
  
  stop
```

# 重启服务
 
```shell  
 ./start.sh
 ./stop.sh
```

搞定