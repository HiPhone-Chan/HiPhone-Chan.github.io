---
layout: post
title: 使用githubpages建立博客
---

使用githubpage搭建个人博客
=======================

# 1 获得存储博客内容的地方

   参考<https://pages.github.com/> ，对个人来说就是生成一个username.github.io的仓库

# 2 搭建一个本地环境

  参考<http://jekyllrb.com/> 搭建一个本地环境(曾经尝试在windows下搭建，感觉各种缺东西，不想折腾就用linux环境吧)，然后根据官网给出的方法执行以下几行命令就可以了

```shell
  gem install jekyll
  jekyll new my-awesome-site
  cd my-awesome-site
  jekyll serve
```

  使用gem时你会与遇到 半天没有响应，这时可以加上 -V 来查看执行过程。

## 2.1 搭建ruby环境

  中途会用到ruby，安装的时候注意ruby的版本，根据官网说明来，不要太低，由于国内原因可能需要切换源，请参考<https://ruby.taobao.org/>，用到如下几条命令

```shell
  gem sources --remove https://rubygems.org/  # 删除源
  gem sources -a https://ruby.taobao.org/     # 添加源
  gem sources -l                              # 列出源
```

## 2.2 使用rvm

  很多时候，系统会帮你安装了一个较低版本的ruby或者不小心装错了版本，或者在软件包里面没有对应版本的ruby，这时使用rvm可比较好的解决这个问题

```shell
  curl -L https://get.rvm.io | bash -s stable
  source ~/.rvm/scripts/rvm
```

  rvm相关命令

```shell
  rvm list         # 查看已安装版本设置信息
  rvm list known   # 列出支持的版本
  rvm list default # 查看当前版本设置信息  
  rvm --default use xxx # 使用xxx版本
```

# 3 分享按钮

  可以使用[jiathis](http://www.jiathis.com/)、[百度分享](http://share.baidu.com/)等，各个系统的优劣就不评价了，看个人喜好吧

# 4 评论功能

可使用[disqus](https://disqus.com/)、[多说](duoshuo.com)、[友言](http://www.uyan.cc/whouse)等，各个系统的优劣就不评价了，看个人喜好吧，一开始随便挑一个用吧

-----

 P.S. 发现使用eclipse来进行博客编写还是不错，因为它集成了git，支持markdown显示，支持html和javascript
