---
title: "扩展 (框架)"
date: 2017-08-30T19:07:05-03:00
weight: 15
menu: main
chapter: true
---


pREST开发用于作为Web框架的可能性，能够基于其API使用它，您可以创建新的端点并放置中间件，根据您的需要调整pREST。

### 简易 Hello World


要为pREST创建自定义模块，您需要扩展路由器并注册自定义新路由。

```go
package main

import (
	"net/http"

	"github.com/prest/adapters/postgres"
	"github.com/prest/cmd"
	"github.com/prest/config"
	"github.com/prest/config/router"
	"github.com/prest/middlewares"
)

func main() {
	config.Load()

	// Load Postgres Adapter
	postgres.Load()

	// Get pREST app
	middlewares.GetApp()

	// Get pPREST router
	r := router.Get()

	// Register custom routes
	r.HandleFunc("/ping", Pong).Methods("GET")

	// Call pREST cmd
	cmd.Execute()
}

func Pong(w http.ResponseWriter, r *http.Request) {
	w.Write([]byte("Pong!"))
}
```