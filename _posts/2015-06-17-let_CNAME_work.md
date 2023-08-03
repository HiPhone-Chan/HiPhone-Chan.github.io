---
layout: post
title: 如何正确的使用CNAME
---

如何正确的使用CNAME
=================

1. 获取在github.io上得到的二级域名对应的IP(可通过ping username.github.io获取)
2. 然后在域名解析的地方加入一条A类型的记录(P.S. 不要添加CNAME类型……)
3. 然后在CNAME文件上添加对应的域名即可，一级，二级域名均可
