---
title: "CORS跨域支持"
date: 2017-08-30T19:06:49-03:00
weight: 14
menu: main
---

在 prest.toml 可以配置 CORS 来允许跨域:

示例:

```
[cors]
alloworigin = ["http://postgres.rest", "http://foo.com"]
```
