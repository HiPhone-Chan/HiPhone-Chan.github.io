---
layout: post
title: 制作docker镜像
categories: tools,docker
tags: docker,images
---

制作docker镜像
==============

# 在线镜像
```
  查看docker id
  docker ps
```

  操作类似git
```
  docker commit {查看docker-id} {本地名称}/{镜像名}:{tagname}
  docker tag {本地名称}/{镜像名}:{tagname} {远程名称}/{镜像名}:{tagname}
  docker push {远程名称}/{镜像名}:{标签}

```

  push前记得login
```
  docker login
```

# 离线镜像
## 导出
```
  docker save -o {文件名}.tar {本地名称}/{镜像名}
```

## 导入
```
  docker load < {文件名}.tar
```
   
# 参考
* docker --help
* https://docs.docker.com/go/guides/