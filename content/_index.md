---
title: "documentation"
weight: 1
---

The _**prestd**_ is open source low-code (aiming to be non-code, with plugin support) to expose database in RESTful API format.

Simplify and accelerate development, instant, realtime, high-performance on any **Postgres** application, **existing or new**.

It started with **PostgreSQL** and we'll stop there, we want to provide quality support on Postgres features. At first we wanted to embrace the world by supporting other databases, but as time went by (gaining experience) we realized that we would not do a good job in even one database.

{{< tip >}}
For this reason we decided to focus on Postgres, if you want to use it with another database (besides postgres) we recommend you to look at [postgres_fdw](https://www.postgresql.org/docs/9.5/postgres-fdw.html).
{{</ tip >}}

[![ProductHunt prestd](https://api.producthunt.com/widgets/embed-image/v1/featured.svg?post_id=303506&theme=light)](https://www.producthunt.com/posts/prest?utm_source=badge-featured&utm_medium=badge&utm_souce=badge-prest)

## Mission

At _**prestd**_, we are on a mission to make the process of new business development faster by making data access _fast, secure and scalable_. We want to reach a world where access to large volumes of data is simple without complex software development!

## Products within the prestd organization

- **[prestd](https://github.com/prest/prest)**: API server, where it all began, giving rise to the other products
- **[Build UI](https://github.com/prest/prest.admin)**: Admin interface for the database, generated automatically from the database schema
- **[bgworker](https://github.com/prest/bgworker)**: Background Worker Processes for PostgreSQL written in Go

---

{{< button "prestd/" "prestd docs" >}}
{{< button "https://github.com/prest/prest" "github" >}}
