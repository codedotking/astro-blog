---
author: huala
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2023-12-21T09:12:47.400Z
title: 网站部署问题
slug: wang-zhan-bu-shu
featured: true
draft: false
tags:
  - 部署
description: 网站部署问题
---

![风景图](@assets/images/posts/image.webp)

## 谷歌 Chrome 浏览器将自动切换为HTTPS链接

项目部署后，有人反映在谷歌Chrome浏览器中访问不了项目，经过调查发现最新版的谷歌浏览器中，在用户访问 http:// 开头的旧链接之后，Chrome 会尝试将其自动跳转至通过加密的 https:// 协议链接到的网站。
而我的网站没有配置https，所以会出现这个问题。

### 解决方案：

使用 [certbot](https://certbot.eff.org) 生成一张 Let's EncryptLet's Encrypt 的免费 HTTPS 证书。

生成证书后，修改 nginx 配置如下：

####

```ssh-config
server {
    listen 80;
    server_name xxx.xxx.xxx; // [!code focus]
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name xxxx.xxx.xxx;

    ssl_certificate /etc/letsencrypt/live/xxxx.xxx.xxx/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/xxxxx.xxx.xxx/privkey.pem;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

然后重启 nginx 即可，重启后在谷歌浏览器中访问项目就会发现地址栏旁边变成一把锁头了。
