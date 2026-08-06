+++
date = '2026-08-05T18:00:03+08:00'
draft = false
title = 'SSL 证书自动续费'
+++

# Ubuntu 安装 Certbot

## 1. 安装 Snap & Certbot

Certbot 官方推荐使用 Snap：

```shell
sudo apt update
sudo apt install -y snapd
```

安装并更新 Snap 核心：

```shell
sudo snap install core
sudo snap refresh core
```

安装新版 Certbot：

```shell
sudo snap install --classic certbot
```

建立命令链接：

```shell
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

验证：

```shell
certbot --version
```

## 2. Nginx 配置

### Nginx 申请证书

Ubuntu 通过 apt 安装的 Nginx

单个

```shell
sudo certbot --nginx -d xxx.example.com 
```

多个

```shell
sudo certbot --nginx -d xxx.example1.com -d xxx.example2.com
```

通过源码安装和多个域名同一张多域名证书

```shell
sudo certbot --nginx \
  --nginx-ctl /usr/local/nginx/sbin \
  --nginx-server-root /usr/local/nginx/conf \
  -d xxx.example1.com \
  -d xxx.example2.com
```

查看证书路径和检查证书到期时间：

```shell
sudo certbot certificates
```

### Nginx 配置

如果有多个域名公用一张证书，默认使用第一个域名名称

```shell
server {
    listen 443 ssl;
    server_name cnfw.emeet.ai;

    ssl_certificate /etc/letsencrypt/live/xxx.example1.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/xxx.example1.com/privkey.pem;

    root /var/www/portal;
    index index.html;
}
```

配完成后

```shell
sudo nginx -t
sudo nginx -s reload
```

## 3. 自动续签脚本

创建续签部署钩子

```shell
sudo mkdir -p /etc/letsencrypt/renewal-hooks/deploy

sudo tee /etc/letsencrypt/renewal-hooks/deploy/reload-nginx.sh >/dev/null <<'EOF'
# !/bin/sh

/usr/sbin/nginx -t && /bin/systemctl reload nginx
EOF

sudo chmod +x /etc/letsencrypt/renewal-hooks/deploy/reload-nginx.sh
```

手动测试脚本：

```shell
sudo /etc/letsencrypt/renewal-hooks/deploy/reload-nginx.sh
```

测试自动续签全过程：

```shell
sudo certbot renew --dry-run
```

检查自动续签定时器：

```shell
systemctl list-timers | grep -i certbot
# 或 Snap 安装时：
sudo systemctl status snap.certbot.renew.timer
```

如果还要确认 Nginx 续签后能自动加载新证书：

```shell
sudo certbot renew --dry-run --run-deploy-hooks
```

---
最终流程就是：

Certbot 定期检查<br>
→ 自动续签证书<br>
→ /etc/letsencrypt/live/... 路径自动更新··<br>
→ 自动 reload Nginx<br>
→ 新证书生效<br>

