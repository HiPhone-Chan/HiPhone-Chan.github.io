nginx配置https
=====

*  拿到https证书，2个文件：一个证书，一个证书key
*  配置nginx如下
```
server {
  listen       443 ssl;
  server_name  域名;

  ssl_certificate      证书路径;
  ssl_certificate_key  证书key路径;

  ssl_session_cache    shared:SSL:1m;
  ssl_session_timeout  5m;

  ssl_ciphers  HIGH:!aNULL:!MD5;
  ssl_prefer_server_ciphers  on;
  # 其他配置
}

```
* 重新加载nginx
```
  nginx -s reload
```

# 参考
https://certbot.eff.org
