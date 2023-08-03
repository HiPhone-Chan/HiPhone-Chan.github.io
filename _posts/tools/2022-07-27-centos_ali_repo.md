---
layout: post
title: centos替换阿里源
categories: tools
tags: centos,repos
---


centos替换阿里源
===============

  Centos8于2021年年底停止服务，在使用yum/dnf源安装时候，会出现下面错误错误：Error: Failed to download metadata for repo 'appstream': Cannot prepare internal mirrorlist: No URLs in mirrorlist

#
```
cd /etc/yum.repos.d/
# 如果是新系统删除原来的文件
rm -rf *
# 下载
wget -O /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
# 或者
curl -o /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo
# 生成缓存
yum makecache
```


# 参考
(CentOS 镜像)[https://developer.aliyun.com/mirror/centos]