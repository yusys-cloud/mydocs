---
title: "使用hugo搭建技术博客"
date: 2022-12-20T18:19:00+08:00
# bookComments: false
# bookSearchExclude: false
---

## 使用hugo搭建技术博客

hugo安装

```
curl -LO https://github.com/gohugoio/hugo/releases/download/v0.108.0/hugo_extended_0.108.0_linux-amd64.tar.gz
mv hugo /usr/local/bin
```

配置Nginx 80转443
```
server {
    listen       80;
    server_name  yangzhiqiang.tech;

    rewrite ^(.*)$ https://${server_name}$1 permanent;
}
```
