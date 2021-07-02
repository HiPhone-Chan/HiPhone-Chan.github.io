https
=====
  certbot可以方便的使用[letsencrypt](https://letsencrypt.org/)项目生成https证书

# 安装使用
```
1 安装snapd(https://snapcraft.io/)
2 确保snad最新sudo snap install core; sudo snap refresh core
3 删除之前安装的cerbbot，根据相应系统输入命令如 sudo apt-get remove certbot, sudo dnf remove certbot, or sudo yum remove certbot.
4 安装certbot sudo snap install --classic certbot
5 添加链接 sudo ln -s /snap/bin/certbot /usr/bin/certbot
6 生成证书，自动配置 sudo certbot --nginx， 如果想手工配置的话sudo certbot certonly --nginx
7 测试自动更新sudo certbot renew --dry-run；Certbot会有自动更新任务运行的，如果没修改服务配置的话，不用再次运行certbbot

```

# 参考
https://certbot.eff.org
