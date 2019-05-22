---
title: "配置"
date: 2017-08-30T19:05:46-03:00
weight: 3
menu: main
---

通过环境变量或者toml文件.

### 环境变量

- PREST\_HTTP_HOST (*default 0.0.0.0*)
- PREST\_HTTP_PORT or PORT (PORT 端口是云因子, **声明时后面这个变量会被覆盖： PREST\_HTTP_PORT**, *默认 3000*)
- PREST\_PG_HOST (*默认 127.0.0.1*)
- PREST\_PG_USER
- PREST\_PG_PASS
- PREST\_PG_DATABASE
- PREST\_PG_PORT (*默认 5432*)
- PREST\_PG_URL or DATABASE\_URL (云因子, **声明时，所有之前的连接字段都会被覆盖**)
- PREST\_JWT_KEY
- PREST\_JWT_ALGO


## TOML
可选的，pREST可被 TOML 文件配置.

- 您可以按照此示例创建自己的`prest.toml`文件，并将其放在运行`prest`命令的同一文件夹中。 

```toml
migrations = "./migrations"

[http]
port = 6000

[jwt]
key = "secret"
algo = "HS256"

[pg]
host = "127.0.0.1"
user = "postgres"
pass = "mypass"
port = 5432
database = "prest"
## or used cloud factor
# URL = "postgresql://user:pass@localhost/mydatabase/?sslmode=disable"

[ssl]
mode = "disable"
sslcert = "./PATH"
sslkey = "./PATH"
sslrootcert = "./PATH"
```

## 授权

- 默认情况下启用JWT中间件。 要禁用JWT，需要将默认值default设置为false。

```toml
[jwt]
default = false
```

```sh
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

- 默认使用 `HS256` 算法.

可以使用环境变量`PREST_JWT_ALGO`或`prest.toml`配置文件的`[jwt]`部分中的`algo`参数来指定JWT算法。


支持的认证算法有：

* The [HMAC signing method](https://en.wikipedia.org/wiki/HMAC): `HS256`,`HS384`,`HS512`
* The [RSA signing method](https://en.wikipedia.org/wiki/RSA_(cryptosystem)): `RS256`,`RS384`,`RS512`
* The [ECDSA signing method](https://en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm): `ES256`,`ES384`,`ES512`


### SSL

- ssl 模式有4种选项:

```toml
"disable" -  # 无 SSL (默认)
"require" - # 总是 SSL (跳过验证)
"verify-ca" - # 总是 SSL (验证服务器提供的证书是否由受信任的CA签名)
"verify-full" - # 总是 SSL (验证服务器提供的证书是否由受信任的CA签名，并且服务器主机名与证书中的名称匹配)
```

### 调试模式

- 在prest.toml文件上设置环境变量 `PREST_DEBUG` or `debug=true`。

```
PREST_DEBUG=true
```

## 迁移

如果 pREST 已设置，`--url` 和 `--path` 标记可选。

```bash
# env var for migrations directory
PREST_MIGRATIONS

# create new migration file in path
prest migrate --url driver://url --path ./migrations create migration_file_xyz

# apply all available migrations
prest migrate --url driver://url --path ./migrations up

# roll back all migrations
prest migrate --url driver://url --path ./migrations down

# roll back the most recently applied migration, then run it again.
prest migrate --url driver://url --path ./migrations redo

# run down and then up command
prest migrate --url driver://url --path ./migrations reset

# show the current migration version
prest migrate --url driver://url --path ./migrations version

# apply the next n migrations
prest migrate --url driver://url --path ./migrations next +1
prest migrate --url driver://url --path ./migrations next +2
prest migrate --url driver://url --path ./migrations next +n

# roll back the previous n migrations
prest migrate --url driver://url --path ./migrations next -1
prest migrate --url driver://url --path ./migrations next -2
prest migrate --url driver://url --path ./migrations next -n

# go to specific migration
prest migrate --url driver://url --path ./migrations goto 1
prest migrate --url driver://url --path ./migrations goto 10
prest migrate --url driver://url --path ./migrations goto v
```
