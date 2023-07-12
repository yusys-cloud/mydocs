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
- docker run --name koishi -p 5140:5140 koishijs/koishi:latest-lite

### workflow
```
docker run --name dagu \
--rm \
-p 8080:8080 \
-v $HOME/.dagu/dags:/home/dagu/.dagu/dags \
-v $HOME/.dagu/data:/home/dagu/.dagu/data \
-v $HOME/.dagu/logs:/home/dagu/.dagu/logs \
yohamta/dagu:latest
```

###  photoview
安装后访问web端口为8000需设置路径默认为 /photos 
```
version: "3"

services:
  db:
    image: mariadb:10.5
    restart: always
    environment:
      - MYSQL_DATABASE=photoview
      - MYSQL_USER=photoview
      - MYSQL_PASSWORD=photosecret
      - MYSQL_RANDOM_ROOT_PASSWORD=1
    volumes:
      - db_data:/var/lib/mysql

  photoview:
    image: viktorstrate/photoview:2
    restart: always
    ports:
      - "8000:80"
    depends_on:
      - db

    environment:
      - PHOTOVIEW_DATABASE_DRIVER=mysql
      - PHOTOVIEW_MYSQL_URL=photoview:photosecret@tcp(db)/photoview
      - PHOTOVIEW_LISTEN_IP=photoview
      - PHOTOVIEW_LISTEN_PORT=80
      - PHOTOVIEW_MEDIA_CACHE=/app/cache
      
      # Optional: If you are using Samba/CIFS-Share and experience problems with "directory not found"
      # Enable the following Godebug
      # - GODEBUG=asyncpreemptoff=1
      
      
      # Optional: To enable map related features, you need to create a mapbox token.
      # A token can be generated for free here https://account.mapbox.com/access-tokens/
      # It's a good idea to limit the scope of the token to your own domain, to prevent others from using it.
      # - MAPBOX_TOKEN=<YOUR TOKEN HERE>

    volumes:
      - api_cache:/app/cache

      # Change This: to the directory where your photos are located on your server.
      # If the photos are located at `/home/user/photos`, then change this value
      # to the following: `/home/user/photos:/photos:ro`.
      # You can mount multiple paths, if your photos are spread across multiple directories.
      - /codes/deploy/static/resources:/photos:ro

volumes:
  db_data:
  api_cache:
  ```