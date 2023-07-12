---
title: "常用开发基础环境清单"
date: 2023-04-04T14:56:48+08:00
# bookComments: false
# bookSearchExclude: false
---

## mvn

```
curl -LO https://dlcdn.apache.org/maven/maven-3/3.9.1/binaries/apache-maven-3.9.1-bin.tar.gz
sudo tar xzvf apache-maven-3.9.1-bin.tar.gz -C /usr/local
export MAVEN_HOME=/usr/local/apache-maven-3.9.1
export PATH=$PATH:$MAVEN_HOME/bin
```

## go语言环境安装