---
date: 2016-04-23T15:21:22+02:00
title: 安装
type: homepage
menu:
  getting-started:
    parent: "getting-started"
weight: 2
---

以下是您可以安装pREST的所有方法，选择最适合您需求的方法。

## Index

1. [下载二进制文件](/getting-started/installation/#downloading-the-binary)
1. [使用Docker](/getting-started/installation/#with-docker)
1. [使用go get](/getting-started/installation/#using-go-get)
1. [通过Homebrew](/getting-started/installation/#with-homebrew)

### 下载二进制文件

对于任何操作系统，您都可以下载最新版本 [这里](https://github.com/prest/prest/releases/latest).

### 使用 Docker

我们只需要从Docker Hub下载pREST镜像：

```sh
docker pull prest/prest
```

### 使用 go get

```sh
go get -u github.com/prest/prest
```

### 使用 Homebrew

如果以上都不适合，你还可以选择使用 [Homebrew](https://brew.sh/)

```sh
brew install prest
```
