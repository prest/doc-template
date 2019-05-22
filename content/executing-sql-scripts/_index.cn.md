---
title: "执行SQL语句"
date: 2017-08-30T19:06:24-03:00
weight: 13
menu: main
---

如果需要执行高级SQL，您可以编写一些脚本SQL并通过pREST访问它们。 这些脚本是模板，您可以通过URL传递值。

_awesome_folder/example_of_powerful.read.sql_:
```sql
SELECT * FROM table WHERE name = "{{.field1}}" OR name = "{{.field2}}";
```

Get 结果:

```
GET /_QUERIES/awesome_folder/example_of_powerful?field1=foo&field2=bar
```

要激活它，您需要为prest.toml中的脚本配置一个位置，如：:

```
[queries]
location = /path/to/queries/
```
### 脚本模板规则

在脚本中，要替换的字段必须如下所示：field1或field2是示例:

```sql
SELECT * FROM table WHERE name = "{{.field1}}" OR name = "{{.field2}}";
```

脚本文件必须具有基于http动词的后缀：

|HTTP Verb|Suffix|
|---|---|
|GET|.read.sql|
|POST|.write.sql|
|PUT, PATCH|.update.sql|
|DELETE|.delete.sql|

在 `queries.location`, 你需要给脚本一个文件夹：


```sh
queries/
└── foo
    └── some_get.read.sql
    └── some_create.write.sql
    └── some_update.update.sql
    └── some_delete.delete.sql
└── bar
    └── some_get.read.sql
    └── some_create.write.sql
    └── some_update.update.sql
    └── some_delete.delete.sql

URLs to foo folder:

GET    /_QUERIES/foo/some_get?field1=bar
POST   /_QUERIES/foo/some_create?field1=bar
PUT    /_QUERIES/foo/some_update?field1=bar
PATCH  /_QUERIES/foo/some_update?field1=bar
DELETE /_QUERIES/foo/some_delete?field1=bar


URLs to bar folder:

GET    /_QUERIES/bar/some_get?field1=foo
POST   /_QUERIES/bar/some_create?field1=foo
PUT    /_QUERIES/bar/some_update?field1=foo
PATCH  /_QUERIES/bar/some_update?field1=foo
DELETE /_QUERIES/bar/some_delete?field1=foo
```

### 模板功能

- *isSet* 如果设置了param，则返回true

```sql
SELECT * FROM table
{{if isSet "field1"}}
WHERE name = "{{.field1}}"
{{end}}
;
```

- *defaultOrValue* 返回参数值或默认值。

```sql
SELECT * FROM table WHERE name = '{{defaultOrValue "field1" "gopher"}}';
```

- *inFormat* 如果param的值是一个切片，则此函数格式为IN SQL子句。
if value of param is an slice this function format to an IN SQL clause.

```sql
SELECT * FROM table WHERE name IN {{inFormat "field1"}};
```