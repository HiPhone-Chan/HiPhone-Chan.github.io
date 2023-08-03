---
layout: post
title: zypper软件源配置
---

zypper软件源配置
==============

# 需要配置的软件源
* Main Repository (OSS)（开源的软件）
* Main Repository (NON-OSS)（非开源软件）
* Main Update Repository（开源软件安全更新）
* Main Update Repository (NON-OSS)（非开源软件安全更新）



```sh
zypper ar   xxxx  # 添加软件源
zypper lr   xxxx  # 查看软件源，加上-d更详细
zypper ref  # 刷新
```

# 参考
zypper -h
