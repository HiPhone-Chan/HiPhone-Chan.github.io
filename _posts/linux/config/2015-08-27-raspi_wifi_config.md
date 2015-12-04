---
layout: post
title: 树莓派设置连上wifi
---

树莓派设置连上wifi
=================

# 加上一个无线网卡

  给树莓派加上一个无线网卡，根据网上推荐使用EDUP，不用再自己折腾驱动了，插上即可用。

# 查看/etc/network/interfaces

  这个基本看一下就可以了，不需要什么修改，我的配置如下

```shell
auto lo

iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
iface default inet dhcp
```

# 修改/etc/wpa_supplicant/wpa_supplicant.conf

  从上一步的配置文件可看到，里面是引用了另外一个文件，我们在这个文件加入自己的配置即可。

```
network={
  ssid="ssid"
  psk="password"
}
```

  就是填上需要连接的wifi信息即可，network可根据需要填写多个。

# 相关命令

* wpa_cli/iwlist - 查看周围热点
* ifup/ifdown - 启动/关闭无线网卡，用于重启
* ifconfig/iwconfig 查看设置相关网卡信息

# 参考
* <http://m.blog.csdn.net/blog/shooter32/45126525>
* <http://blog.csdn.net/xukai871105/article/details/38170513>
