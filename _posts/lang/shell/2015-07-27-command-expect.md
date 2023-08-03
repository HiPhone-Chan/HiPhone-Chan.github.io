---
layout: post
title: expect实现自动交互
categories: shell
tags: shell
---

#expect实现自动交互#
   
   在写脚本的过程中可能会遇到一些需要人机交互的命令，这令自动化带来了不便。使用expect可解决这个问题。省去各种复杂的参数，expect可简单的用如下方式进行使用，其中cmd是个命令字符串。
   
```shell
   expect -c cmd
```
  
  expect也可以写成脚本，通过以下例子来对常用易用的命令进行说明。expect用的是tcl((Tool Command Language)语法，其中常用的命令有spawn, send, expect, and interact，以下面的例子进行说明。下面的例子实现了用ssh对远程主机进行操作.
  
```
#!/usr/bin/expect

set timeout 30
set user [lindex $argv 0]
set ip [lindex $argv 1]
set pwd [lindex $argv 2]
set cmd [lindex $argv 3]

if {$cmd == ""} {
  set cmd exit
}

spawn -noecho ssh ${user}@${ip} ${cmd}
expect {
  (yes/no)? {
    send "yes\r"
    exp_continue
  } Password: {
    stty -echo
    send ${pwd}\r
    stty echo
  } timeout: {
    send_user "time out\n"
    exit
  } eof {
    #exit $expect_out(1, string)
  }
}

interact

```

1. 首行像shell一样标明执行脚本的程序，路径可以通过which expect查得
2. 变量通过set语句进行赋值，通过${}来获取
3. tcl语法对if等语句限制比较紧，需要的地方必须有空格
4. spawn语句起了一个子进程来执行后面的命令，-noecho 选项可以禁止控制台输出
5. expect(和expect命令不一样，是expect内置的语句)用来对响应的语句进行捕获，捕获后进行相关操作，选项-re表示使用正在表达式匹配，选项-ex表示使用精确匹配
6. send语句用来进行相关输入
7. interact语句标明在进行相关操作后将操作权返还给用户
8. exit表示程序退出
9. 脚本的入参存放在argv中，可通过[llist $argv n]或者[lrange $argv n n]来获取第n个参数，argv0则表示脚本名称
10. spawn scp ${srcfile} ${user}@${ip}:${destfile}可通过这个语句来传输文件
#参考
* man expect
