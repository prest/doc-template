---
title: "Custom middlewares"
date: 2017-02-28T16:05:05-03:00
weight: 15
chapter: true
---

使用前面的示例，我们可以将我们的中间件创建为一个函数并使用 `GetApp()` ([godocs.org at prest/middlewares](https://godoc.org/github.com/prest/middlewares#GetApp)) 返回 `*negroni.Negroni` 对象.

```go
package main

import (
	"log"
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
	n := middlewares.GetApp()

	// Register custom middleware
	n.UseFunc(CustomMiddleware)

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

func CustomMiddleware(w http.ResponseWriter, r *http.Request, next http.HandlerFunc) {
	log.Println("Calling custom middleware")
	next(w, r)
}
```

### 重排序中间件

也可以更改中间件的执行顺序, 我们有 `middlewares.MiddlewareStack` ([godocs.org at prest/middlewares](https://godoc.org/github.com/prest/middlewares#pkg-variables)) 接收 `negroni.Handler` ，当你传递一个新顺序的数组。

```go
package main

import (
	"log"
	"net/http"


	"github.com/prest/adapters/postgres"
	"github.com/prest/cmd"
	"github.com/prest/config"
	"github.com/prest/config/router"
	"github.com/prest/middlewares"
	"github.com/urfave/negroni"
)

func main() {
	config.Load()
	// Load Postgres Adapter
	postgres.Load()
	// Reorder middlewares
	middlewares.MiddlewareStack = []negroni.Handler{
		negroni.Handler(negroni.NewRecovery()),
		negroni.Handler(negroni.NewLogger()),
		negroni.Handler(middlewares.HandlerSet()),
		negroni.Handler(negroni.HandlerFunc(CustomMiddleware)),
	}

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

func CustomMiddleware(w http.ResponseWriter, r *http.Request, next http.HandlerFunc) {
	log.Println("Calling custom middleware")
	next(w, r)
}
```
