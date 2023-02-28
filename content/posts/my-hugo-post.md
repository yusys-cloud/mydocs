---
title: "使用hugo搭建技术博客"
date: 2022-12-20T18:19:00+08:00
# bookComments: false
# bookSearchExclude: false
---

## 使用hugo搭建技术博客

Hugo 是一个用Go 编写的静态网站生成器。简单、易用、高效、易扩展、快速部署

### Hugo安装
```
curl -LO https://github.com/gohugoio/hugo/releases/download/v0.108.0/hugo_extended_0.108.0_linux-amd64.tar.gz
mv hugo /usr/local/bin
```
### hugo基础使用
- 创建站点
```
hugo new site quickstart
cd quickstart
```
- 创建文章,content目录中存放md格式文章
```
hugo new posts/my-first-post.md
```
- 使用皮肤,hugo提供较多的themes可选择,[更多参考](https://themes.gohugo.io/)
```
git submodule add https://github.com/alex-shpak/hugo-book themes/hugo-book
```
- 发布站点,public目录生成HTML静态资源,也可使用hugo server提供的PageLive
```
hugo
```

## Nginx 配置

### SSL配置
通过[免费HTTPS证书](https://freessl.cn/)生成后，配置到Nginx
```
server {
    listen       443 ssl;
    server_name  yangzhiqiang.tech;

    ssl_certificate  	/root/.acme.sh/yangzhiqiang.tech/yangzhiqiang.tech.cer;
    ssl_certificate_key /root/.acme.sh/yangzhiqiang.tech/yangzhiqiang.tech.key;

    index index.html;

    location / {
	    add_header Access-Control-Allow-Origin *;
        add_header Access-Control-Allow-Headers X-Requested-With;
        add_header Access-Control-Allow-Methods GET,POST,OPTIONS;
        index index.html;
        root /wwww/mydocs/public/;
     }
    error_page 404               /index.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
```

### 配置Nginx 80转443
```
server {
    listen       80;
    server_name  yangzhiqiang.tech;

    rewrite ^(.*)$ https://${server_name}$1 permanent;
}
```

## 配置GitHub workflow 自动发布

### 生产ssh私钥
```
ssh-keygen -m PEM -t rsa -b 4096
```

### 使用ssh发布插件
```
	- name: Deploy to Server
        uses: easingthemes/ssh-deploy@main
        env:
            SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}
            ARGS: "-rlgoDzvc -i --delete"
            SOURCE: "./public"
            REMOTE_HOST: ${{ secrets.REMOTE_HOST }}
            REMOTE_USER: ${{ secrets.REMOTE_USER }}
            TARGET: ${{ secrets.REMOTE_TARGET }}
```

## Ubuntu配置用户
### 新增用户
```
sudo userdel yzq
sudo useradd yzq -d /home/yzq -m
cat /etc/passwd | grep yzq
```
### 设置/bin/bash

```
sudo vi /etc/passwd
```

### 设置账号账号密码可远程登录 PasswordAuthentication一项，将其改为 yes

```
sudo vim /etc/ssh/sshd_config
sudo service ssh restart
```
