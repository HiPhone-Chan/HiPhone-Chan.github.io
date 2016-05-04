---
layout: post
title: shell条件表达式
categories: shell
tags: shell
---

shell条件表达式
==============

  以下是从man bash出来的文档，并对相关文字进行翻译(持续更新)

* -a file 为真条件：文件存在。
* -b file True if file exists and is a block special file.
* -c file True if file exists and is a character special file.
* -d file 为真条件：文件存在并且文件是个目录(文件夹)。
* -e file 为真条件：文件存在。
* -f file True if file exists and is a regular file.
* -g file True if file exists and is set-group-id.
* -h file True if file exists and is a symbolic link.
* -k file True if file exists and its ``sticky'' bit is set.
* -p file True if file exists and is a named pipe (FIFO).
* -r file 为真条件：文件存在并且文件可读。
* -s file True if file exists and has a size greater than zero.
* -t fd   True if file descriptor fd is open and refers to a terminal.
* -u file True if file exists and its set-user-id bit is set.
* -w file 为真条件：文件存在并且文件可写。
* -x file 为真条件：文件存在并且文件可执行。
* -O file True if file exists and is owned by the effective user id.
* -G file True if file exists and is owned by the effective group id.
* -L file True if file exists and is a symbolic link.
* -S file True if file exists and is a socket.
* -N file True if file exists and has been modified since it was last read.
* file1 -nt file2 为真条件：文件1比文件2新(根据修改日期)，或者文件1存在文件2不存在。
* file1 -ot file2 为真条件：文件1比文件2旧，或者文件1不存在文件2存在。
* file1 -ef file2 为真条件：文件1和2指向相同设备 (device)和索引节点(inode numbers).
* -o optname True  if shell option optname is enabled.  See the list of options under the description of the -o option to the set builtin below.
* -z string 为真条件：字符串长度为零。
* -n string 为真条件：字符串长度不为零。
* string1 == string2 为真条件：字符串相等。  = may be used in place of == for strict POSIX compliance.
* string1 != string2 为真条件：字符不串相等。
* string1 < string2 True if string1 sorts before string2 lexicographically in the current locale.
* string1 > string2 True if string1 sorts after string2 lexicographically in the current locale.

* arg1 OP arg2 arg1和arg2为整数，OP包括
- -eq 等于
- -ne 不等于
- -lt 小于
- -le 小于等于
- -gt 大于
- -ge 大于等于
