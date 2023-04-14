---
title: "常用docker清单"
date: 2023-04-04T14:56:48+08:00
# bookComments: false
# bookSearchExclude: false
---

## docker导入导出

```
5.7.14
docker save quay.io/metallb/controller:v0.12.1 quay.io/metallb/speaker:v0.12.1 | gzip -c > metallb-images.tar.gz
docker save mysql:5.7.14 | gzip -c > images.tar.gz
docker load --input images.tar.gz
```

## 常用docker清单

- docker run --name mysql -p 3306:3306 -v /home/app/data/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=admin -d mysql:5.7
- docker run --name mysql -p 3306:3306  -e MYSQL_ROOT_PASSWORD=admin -d mysql:5.7
- docker run --name nacos -e MODE=standalone -p 8848:8848 -p 9848:9848 -d nacos/nacos-server:2.0.2
