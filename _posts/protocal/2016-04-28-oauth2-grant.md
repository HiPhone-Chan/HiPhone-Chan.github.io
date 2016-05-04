---
layout: post
title: Oauth2.0 的几种认证方式
categories: protocol
---

# Oauth2.0 的几种认证方式

# 名词解释

- Client - 客户，如第三方应用
- User Agent - 用户代理，如浏览器
- Resource Owner - 资源拥有者，如用户
- Authorization server - 授权服务器，服务提供商用来授权的服务器
- Resource server - 资源服务器，服务提供商存放用户资源的服务器

# 授权码认证(Authorization Code Grant)

```
+----------+
| Resource |
|   Owner  |
|          |
+----------+
     ^
     |
    (B)
+----|-----+          Client Identifier      +---------------+
|         -+----(A)-- & Redirection URI ---->|               |
|  User-   |                                 | Authorization |
|  Agent  -+----(B)-- User authenticates --->|     Server    |
|          |                                 |               |
|         -+----(C)-- Authorization Code ---<|               |
+-|----|---+                                 +---------------+
  |    |                                         ^      v
 (A)  (C)                                        |      |
  |    |                                         |      |
  ^    v                                         |      |
+---------+                                      |      |
|         |>---(D)-- Authorization Code ---------'      |
|  Client |          & Redirection URI                  |
|         |                                             |
|         |<---(E)----- Access Token -------------------'
+---------+       (w/ Optional Refresh Token)
```

  授权码认证是功能最完整、流程最严密的授权模式

- (A) 客户通过用户代理，用户代理讲重定向到授权服务器
- (B) 客户选择授予的权限
- (C) 授权服务器将重定向到客户之前指定的重定向URI上，并返回授权码
- (D) 客户使用授权码和重定向URI向授权服务器请求Access Token
- (E) 授权服务器返回Access Token

## 请求参数

### 授权请求
- response_type(必选)  值为 "code".
- client_id(必选)
- redirect_uri(可选)
- scope(可选) 请求范围
- state(建议) 用于保持请求和返回的状态，以防跨站请求伪造

### 请求获取Access Token
- grant_type(必选)  值为 "authorization_code".
- code(必选)  从授权服务器获得的code
- redirect_uri(必选)
- client_id(必选)

## 请求样例

```
# 初次请求授权，会重定向到授权服务器
GET /authorize?response_type=code&client_id=s6BhdRkqt3&state=xyz
       &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
   Host: server.example.com

# 用户获取Access Token
POST /token HTTP/1.1
   Host: server.example.com
   Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
   Content-Type: application/x-www-form-urlencoded

   grant_type=authorization_code&code=SplxlOBeZQQYbYS6WxSbIA
   &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb
```

# 隐式认证(Implicit Grant)

```
+----------+
| Resource |
|  Owner   |
|          |
+----------+
     ^
     |
    (B)
+----|-----+          Client Identifier     +---------------+
|         -+----(A)-- & Redirection URI --->|               |
|  User-   |                                | Authorization |
|  Agent  -|----(B)-- User authenticates -->|     Server    |
|          |                                |               |
|          |<---(C)--- Redirection URI ----<|               |
|          |          with Access Token     +---------------+
|          |            in Fragment
|          |                                +---------------+
|          |----(D)--- Redirection URI ---->|   Web-Hosted  |
|          |          without Fragment      |     Client    |
|          |                                |    Resource   |
|     (F)  |<---(E)------- Script ---------<|               |
|          |                                +---------------+
+-|--------+
  |    |
 (A)  (G) Access Token
  |    |
  ^    v
+---------+
|         |
|  Client |
|         |
+---------+
```

  隐式认证跳过了授权码的部分，直接在用户代理完成获取token的操作。

- (A) 客户通过用户代理，用户代理讲重定向到授权服务器
- (B) 客户选择授予的权限
- (C) 授权服务器将重定向到客户之前指定的重定向URI上，并返回Access Token
- (D) 用户代理重定向到客户资源网站
- (E) 客户资源网站返回脚本
- (F) 用户代理执行脚本获得Access Token
- (G) 用户代理返回Access Token

## 请求参数

### 授权请求
- response_type(必选)  值为 "token".
- client_id(必选)
- redirect_uri(可选)
- scope(可选) 请求范围
- state(建议) 用于保持请求和返回的状态，以防跨站请求伪造

### 请求获取Access Token
- grant_type(必选)  值为 "authorization_code".
- code(必选)  从授权服务器获得的code
- redirect_uri(必选)
- client_id(必选)

## 请求样例

```
# 初次请求，会重定向到授权服务器，在之后的重定向返回中会获得Access Token
GET /authorize?response_type=token&client_id=s6BhdRkqt3&state=xyz
        &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1
    Host: server.example.com
```

# 密码认证(Resource Owner Password Credentials Grant)

```
+----------+
| Resource |
|  Owner   |
|          |
+----------+
     v
     |    Resource Owner
    (A) Password Credentials
     |
     v
+---------+                                  +---------------+
|         |>--(B)---- Resource Owner ------->|               |
|         |         Password Credentials     | Authorization |
| Client  |                                  |     Server    |
|         |<--(C)---- Access Token ---------<|               |
|         |    (w/ Optional Refresh Token)   |               |
+---------+                                  +---------------+
```

  用户通过将用户名和密码带给客户端来获取accessToken。由于客户可以获取用户的密码，一般用于用户信得过的第三方应用。

- (A) 资源拥有者向客户发送密码认证信息
- (B) 客户将资源拥有者的密码认证信息发给授权服务器
- (C) 授权服务器返回Access Token

## 请求参数

- grant_type(必选) 值为"password"
- username(必选) 资源拥有者用户名
- password(必选) 资源拥有者密码
- scope(可选)

## 请求样例

```
# 请求获取Access Token
POST /token HTTP/1.1
     Host: server.example.com
     Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
     Content-Type: application/x-www-form-urlencoded

     grant_type=password&username=uuuuu&password=ppppp
```

# 客户凭证认证(Client Credentials Grant)

```
+---------+                                  +---------------+
|         |                                  |               |
|         |>--(A)- Client Authentication --->| Authorization |
| Client  |                                  |     Server    |
|         |<--(B)---- Access Token ---------<|               |
|         |                                  |               |
+---------+                                  +---------------+
```

客户端直接从授权服务器获取token，已经和用户的用户名密码没什么关系了。

- (A) 客户向授权服务器请求Access Token
- (B) 授权服务器返回Access Token

## 请求参数

- grant_type(必选) 值为"client_credentials"
- scope(可选)

## 请求样例

```
# 请求获取Access Token
POST /token HTTP/1.1
     Host: server.example.com
     Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
     Content-Type: application/x-www-form-urlencoded

     grant_type=client_credentials
```

# 扩展授权(Extension Grants)

通过使用绝对URI来作为grant_type的值来使用此功能，并且可以根据需要使用任意额外的需要的参数。

## 请求样例

```
POST /token HTTP/1.1
     Host: server.example.com
     Content-Type: application/x-www-form-urlencoded

     grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Asaml2-
     bearer&assertion=PEFzc2VydGlvbiBJc3N1ZUluc3RhbnQ9IjIwMTEtMDU
     [...omitted for brevity...]aG5TdGF0ZW1lbnQ-PC9Bc3NlcnRpb24-
```

# Demo

  此Demo的授权服务器实现是基于Spring Oauth的。  
  地址为：<https://github.com/HiPhone-Chan/Oauth-Authorization-demo>

--------------------------------------------------------------------------------

# 参考

- [Oauth2](https://tools.ietf.org/html/draft-ietf-oauth-v2-31)
