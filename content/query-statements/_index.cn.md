---
title: "查询语句"
date: 2017-08-30T19:06:04-03:00
weight: 12
menu: main
---

### 条件查询过滤Filter (WHERE)

```
GET /DATABASE/SCHEMA/TABLE?FIELD=$eq.VALUE
```

查询运算符：

| Name | 描述 |英文表述|
|----|----|-------------|
| $eq | 相等| Matches values that are equal to a specified value.|
| $gt | 大于|Matches values that are greater than a specified value.|
| $gte |大于等于| Matches values that are greater than or equal to a specified value.|
| $lt | 小于|Matches values that are less than a specified value.|
| $lte |小于等于| Matches values that are less than or equal to a specified value.|
| $ne | 不等于|Matches all values that are not equal to a specified value.|
| $in | 包含|Matches any of the values specified in an array.|
| $nin | 不包含|Matches none of the values specified in an array.|
| $null | 空值|Matches if field is null.|
| $notnull | 非空|Matches if field is not null.|
| $true | 为真|Matches if field is true.|
| $nottrue |不为真| Matches if field is not true.|
| $false |为伪| Matches if field is false.|
| $notfalse |不为伪| Matches if field is not false.|
| $like |整个字符串匹配| Matches always cover the entire string.|
| $ilike |同上，不区分大小写| Matches *case-insensitive* always cover the entire string.|


### 条件查询过滤Filter (WHERE) with JSONb field

```
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?FIELD->>JSONFIELD:jsonb=VALUE (filter)
```

### 选择 Select - GET

```
http://127.0.0.1:8000/databases (show all databases)
http://127.0.0.1:8000/databases?_count=* (count all databases)
http://127.0.0.1:8000/databases?_renderer=xml (JSON by default)
http://127.0.0.1:8000/schemas (show all schemas)
http://127.0.0.1:8000/schemas?_count=* (count all schemas)
http://127.0.0.1:8000/schemas?_renderer=xml (JSON by default)
http://127.0.0.1:8000/tables (show all tables)
http://127.0.0.1:8000/tables?_renderer=xml (JSON by default)
http://127.0.0.1:8000/DATABASE/SCHEMA (show all tables, find by schema)
http://127.0.0.1:8000/DATABASE/SCHEMA?_renderer=xml (JSON by default)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE (show all rows, find by database and table)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_select=column (select statement by columns)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_select=column[array id] (select statement by array colum)

http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_select=* (select all from TABLE)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_count=* (use count function)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_count=column (use count function)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_page=2&_page_size=10 (pagination, page_size 10 by default)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?FIELD=VALUE (filter)
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?_renderer=xml (JSON by default)


Select operations over a VIEW
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_select=column (select statement by columns in VIEW)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_select=* (select all from VIEW)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_count=* (use count function)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_count=column (use count function)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_page=2&_page_size=10 (pagination, page_size 10 by default)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?FIELD=VALUE (filter)
http://127.0.0.1:8000/DATABASE/SCHEMA/VIEW?_renderer=xml (JSON by default)

```

### 新增 Insert - POST

```
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE
```

JSON DATA:
```
{
    "FIELD1": "string value",
    "FIELD2": 1234567890
}
```

### 更新 Update - PATCH/PUT

Using query string to make filter (WHERE), example:

```
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?FIELD1=xyz
```

JSON DATA:
```
{
    "FIELD1": "string value",
    "FIELD2": 1234567890,
    "ARRAYFIELD": ["value 1","value 2"]
}
```
### 删除 Delete - DELETE

Using query string to make filter (WHERE), example:

```
http://127.0.0.1:8000/DATABASE/SCHEMA/TABLE?FIELD1=xyz
```

## 连接 JOIN

```
/DATABASE/SCHEMA/Table?_join=Type:Table2:Table.field:Operator:Table2.field
```
Parameters:

1. Type (INNER, LEFT, RIGHT, OUTER)
1. Table2
1. Table.field
1. Operator ($eq, $lt, $gt, $lte, $gte)
1. Table2.field

Using query string to JOIN tables, example:

```
/DATABASE/SCHEMA/friends?_join=inner:users:friends.userid:$eq:users.id
```
## 查询运算符：

| Name | 描述 |英文表述|
|----|----|-------------|
| $eq | 相等| Matches values that are equal to a specified value.|
| $gt | 大于|Matches values that are greater than a specified value.|
| $gte |大于等于| Matches values that are greater than or equal to a specified value.|
| $lt | 小于|Matches values that are less than a specified value.|
| $lte |小于等于| Matches values that are less than or equal to a specified value.|
| $ne | 不等于|Matches all values that are not equal to a specified value.|
| $in | 包含|Matches any of the values specified in an array.|
| $nin | 不包含|Matches none of the values specified in an array.|



## 去重DISTINCT 

要在查询中使用 *DISTINCT* 子句, 需要附加 `_distinct=true`.

Examples:
```
    GET /DATABASE/SCHEMA/TABLE/?_distinct=true
```

## 排序
在查询中使用 *ORDER BY* 您必须在 *GET* 请求中传入带有fieldname（s）的属性`_order`作为值。 对于 *倒序 DESC* 命令，请使用前缀`-`。 对于 *multiple* 多重排序，字段用逗号分隔。



示例:

### 正序
    GET /DATABASE/SCHEMA/TABLE/?_order=fieldname

### 倒序
    GET /DATABASE/SCHEMA/TABLE/?_order=-fieldname

### 多重排序
    GET /DATABASE/SCHEMA/TABLE/?_order=fieldname01,-fieldname02,fieldname03

## 分组

支持以下方法：

| name | Use in request |中文|
| ------- | ------------- |------ |
| SUM | sum:field |求和|
| AVG | avg:field |求平均|
| MAX | max:field |求最大|
| MIN | min:field |求最小|
| MEDIAN | median:field |求中值|
| STDDEV | stddev:field |求标准差|
| VARIANCE | variance:field |求方差|

### 示例:
	GET /DATABASE/SCHEMA/TABLE/?_select=fieldname00,fieldname01&_groupby=fieldname01

#### 分组方法
	GET /DATABASE/SCHEMA/TABLE/?_select=fieldname00,sum:fieldname01&_groupby=fieldname01

#### 支持Having 
要在**Group By** 使用 Having ，使用以下语法:

	_groupby=fieldname->>having:GROUPFUNC:FIELDNAME:CONDITION:VALUE-CONDITION

示例:

	GET /DATABASE/SCHEMA/TABLE/?_select=fieldname00,sum:fieldname01&_groupby=fieldname01->>having:sum:fieldname01:$gt:500
