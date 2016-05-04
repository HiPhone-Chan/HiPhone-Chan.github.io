---
layout: post
title: ngnix 简单负载均衡配置
---

ngnix 简单负载均衡配置
====================

# 对ngnix.conf进行配置

```shell
    upstream chf.com {
        server 127.0.0.1:8088;
        server 127.0.0.1:8099;
    }

    server {
        listen 8080;
        server_name  chf.com; #用于标识server

        location / {
            proxy_pass   http://chf.com;
            proxy_set_header  x-forwarded-for $proxy_add_x_forwarded_for; // 设置请求头
            add_header  'Access-Control-Allow-Origin' '*'; // 设置响应头
        }
    }
```

## ngnix对websocket进行代理

  需要显式的设置Upgrade和Connection的头信息
```shell
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection "upgrade";
```

# 相关命令

* ngnix -s reload #重新加载配置文件
* ngnix -? #查看详细使用


# 参考
* <https://www.nginx.com/products/application-load-balancing/>
