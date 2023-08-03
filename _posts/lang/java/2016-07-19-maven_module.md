---
layout: post
title: 使用maven打对module打包
categories: java
---

使用maven打对module打包
======================

  如果maven项目有多个子模块，当只想打包某几个子模块，需要用到以下的maven选项。

```
-pl, --projects
  用于指定需要构建的子模块
-am, --also-make
  同时构建子模块依赖的其他模块
-amd, --also-make-dependents
  同时构建依赖这个子模块的其他模块
```

# 示例
```sh
   mvn package -pl module-common -am -amd
```

# 更新子模块版本

```sh
  mvn versions:set -DnewVersion=1.0.1-SNAPSHOT
```


# 参考
  mvn -h
