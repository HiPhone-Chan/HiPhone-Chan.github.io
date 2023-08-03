---
layout: post
title: Oauth2.0 state的说明
categories: protocol
---

# Oauth2.0 state的理解

  Oauth2.0 state的作用网上有说明，但是大多都是文字描述，难以理解，这里整理一下做个说明。

  正常的Oauth2.0流程如下图，一般来说没什么问题。
  ![template](/images/protocol/oauth2.png)

  如果不带上state，如下图所示，问题出在万一用户不小心使用了伪造的网站或者app应用，这些恶意会模仿进行第三方授权，过程和正常流程一样，只是最后获得的用户信息不是用户本人的，但是对于用户来说他会以为是自己的，这样后面所有的操作都会操作这个错误的用户，从而导致各种问题，像把钱充到这个账号。
  ![template](/images/protocol/oauth2-csrf.png)

  如果带上state并校验，如下图所示，就算用户不小心使用了伪造的网站，由于最后state校验不通过，用户登录失败，从而避免上述的问题。
  ![template](/images/protocol/oauth2-state.png)