---
title: "权限"
date: 2017-08-30T19:06:32-03:00
weight: 13
menu: main
---

### 限制模式
在 prest.toml 中，您可以配置每个表的读/写/删除权限。

```
[access]
restrict = true  # 只能访问下面列出的表格
```

`restrict = false`: (默认) 将以发布模式提供服务。 您可以在没有配置权限的情况下编写/读取/删除每个数据。

`restrict = true`: 您需要配置所有表的权限。

### 表权限

示例:

```
[[access.tables]]
name = "test"
permissions = ["read", "write", "delete"]
fields = ["id", "name"]
```

同一个表的多个配置：

```
[access]
restrict = true  # can access only the tables listed below

    [[access.tables]]
    name = "test"
    permissions = ["read"]
    fields = ["id", "name"]

    [[access.tables]]
    name = "test"
    permissions = ["write"]
    fields = ["name"]
```

|attribute|description|中文|
|---|---|---|
|table|Table name|表格名|
|permissions|Table permissions. Options: `read`, `write` and `delete`|表权限：3个选项读写删|
|fields|Fields permitted for operations|允许操作的字段|


配置示例: [prest.toml](https://github.com/prest/prest/blob/master/testdata/prest.toml)
