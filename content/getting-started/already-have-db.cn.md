---
date: 2016-04-23T15:21:22+02:00
title: 已有数据库
type: homepage
menu:
  getting-started:
    parent: "running"
weight: 4
---

有四种情况来安装pREST，主要分下面2种方式：

1. [二进制、homebrew、go get](/getting-started/running/#with-the-binary-or-homebrew-or-go-get)
1. [Docker 或 Docker Compose](/getting-started/running/#with-docker)


### 二进制、homebrew、go get

如果通过下载二进制文件或使用Homebrew或使用go get安装pREST，则必须按如下方式传递必要的二进制变量：

```sh
PREST_PG_USER=postgres \
PREST_PG_DATABASE=prest \
PREST_PG_PORT=5432 \
PREST_HTTP_PORT=3010 \
prest # Binary installed
```

### 通过 docker

已经完成了上一步的拉取，所以：

```sh
docker run -e PREST_HTTP_PORT=3000 \
	-e PREST_PG_HOST=127.0.0.1 \
	-e PREST_PG_USER=postgres \
	-e PREST_PG_PASS=pass \
	prest/prest
```
或者使用 Docker Compose (这里是[示例代码](https://github.com/prest/prest/blob/master/docker-compose.yml))

```sh
docker-compose up
```

有关配置和其他环境变量的更多详细信息参见 [配置](/configurations)
